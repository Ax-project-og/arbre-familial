# CONVERSION.md — passer le document réel au modèle de `proto.html`

Lire `CLAUDE.md` d'abord.

## 1. Le but

`index.html` était **écrit à la main** : 30 fiches positionnées en absolu, 26 tracés SVG en coordonnées littérales, 8 pastilles de mariage et 5 losanges d'union posés au pixel. Chaque ajout de personne oblige à recalculer des chemins à la main, et le document ne *sait* pas qui descend de qui.

`proto.html` démontre l'architecture cible sur des données fictives : **les données d'un côté, le moteur de l'autre**. Les fiches, les fils, les bandes de génération, la colonne des chiffres romains et la hauteur de la scène sont calculés au chargement à partir d'un objet JavaScript. Seules les **positions restent posées à la main**, parce que la composition est éditoriale et qu'un placement automatique ferait un arbre correct et sans point de vue.

**La conversion consiste à porter le contenu réel dans ce moteur, sans rien perdre et sans changer l'apparence.**

## 2. Ce qui ne doit pas changer

- **Fichier unique, sans dépendance.** Pas de npm, pas de build, pas de CDN, pas de framework. Le fichier s'ouvre au double-clic et fonctionne hors ligne.
- **Pas de `localStorage` ni de stockage navigateur.**
- **L'apparence.** Mêmes couleurs, mêmes polices, mêmes fiches, mêmes fils orthogonaux, mêmes pastilles. Un lecteur ne doit pas voir la différence au premier coup d'œil — seulement découvrir qu'on peut cliquer.
- **Les conventions documentaires** de `CLAUDE.md` § 3, à l'identique.
- **Le texte.** Aucune reformulation des transcriptions, des gloses, des encarts, des pistes de recherche. La conversion est structurelle, pas rédactionnelle.
- **Les deux onglets existants** et tout le contenu du `dossier` et des `footnotes`, qui restent en HTML statique dans cette étape.

## 3. Ce que `proto.html` apporte, et qu'il faut reprendre

1. `PERSONNES` / `UNIONS` / `ACTES` : trois tableaux, en bas du fichier, seule zone à éditer après chaque séance.
2. **Fiches et fils générés** — `renderCards()` puis `layout()`, qui mesure les fiches réellement posées (`offsetLeft/offsetTop/offsetHeight`) et en déduit tracés, pastilles, losanges, bandes et rails. Déplacer une fiche ne casse plus rien.
3. **Surbrillance de lignée** — clic sur une personne : descendance en bronze, ascendance en vert-de-gris, conjoints entrés par alliance en anneau pâle, le reste estompé. Les bordures gardent leur sens documentaire ; la lumière passe par un anneau et un fond teinté.
4. **Tiroir latéral** — chronologie déduite des données (naissance, domiciles, métiers, mariages, naissances des enfants, décès, avec l'âge calculé), récit, réserves, dossier d'actes, parenté cliquable. La fiche de l'arbre ne garde que naissance, métier, conjoint, décès.
5. **Actes comme objets** : un acte nomme plusieurs personnes, chacune à un titre. D'où « son dossier » vs « **apparaît aussi dans** », et, dans les transcriptions, la liste des personnes nommées.
6. **Parenté relative** — un sélecteur « point de vue » ; chaque fiche annonce ce que la personne est pour ce point de vue.
7. **Modes d'affichage** — *Arbre*, *Preuves* (densité documentaire), *Nouveautés* (apports de la dernière séance).
8. **Frise** (onglet séparé, à l'essai), **liens profonds** `#p=identifiant`, **recherche**, **glisser pour explorer**, mode `?audit`.

## 4. Le modèle de données à écrire

Reprendre exactement la forme du proto, en l'étendant sur trois points imposés par le dossier réel.

```js
{
  id:"francois-amiot-1780",         // stable, jamais réutilisé : sert aux liens #p=
  prenoms:"François", nom:"AMIOT",
  f:false,                          // féminin -> accords automatiques
  gen:2,                            // index dans GENERATIONS (−2 = 0, −1 = 1, 0 = 2, I = 3…)
  x:170, y:569, w:230,              // reprises telles quelles du fichier actuel
  doute:false,                      // fiche à confirmer -> pointillé rouge
  naissance:{date:"24/12/1780", lieu:"Mont-le-Frânois", incertain:false},
  deces:{date:"18/03/1839", heure:"6 h", lieu:"Vars", age:"58 ans"},
  metiers:[{quoi:"cordonnier", an:1803},{quoi:"propriétaire", an:1818}],
  lieux:[{quoi:"…", an:1803}],
  recit:["…"],                      // paragraphes du tiroir
  notes:[{t:"À vérifier", b:"…", doute:true}],
  neuf:true                         // apporté par la dernière séance
}
```

**Extension 1 — filiations multiples et qualifiées.** `parents` ne peut pas être un simple identifiant d'union. Prévoir :

```js
filiations:[
  {union:"u-carpentier-josephine", statut:"reconnaissance annulée", du:"1892", au:"1897"},
  {union:"u-theolinde", statut:"adoptive", du:"1906"},
  {mere:"josephine-grillot", statut:"naturelle"}      // filiation sans union
]
```

Yvonne est le cas d'école ; le moteur doit pouvoir dire *laquelle* compte pour tracer le fil, et lesquelles s'affichent dans le tiroir. Par défaut : filiation biologique pour la lignée, toutes les filiations listées dans le tiroir.

**Extension 2 — unions qualifiées.** `{id, epoux:[a,b], enfants:[…], mariage:"26/04/1803", lieu:"Vars", acte:"6 floréal an XI", rang:1, statut:"probable"|"établie", tr:"t-…"}`. `rang` sert aux deux mariages de Joséphine ; `statut:"probable"` donne le trait pointillé (union RIBAUT × VILLETTE de 1930, second mariage de François AMIOT).

**Extension 3 — les actes manquants sont des données.** `{id, type:"x", manquant:true, titre:"…", note:"pourquoi on ne l'a pas, où chercher", mentions:[…]}`. C'est ce qui alimente le mode *Preuves* et rejoint les pistes de recherche.

Chaque acte : `{id, type:"n"|"m"|"d"|"x", an, date, lieu, cote, tr:"identifiant de transcription", neuf, mentions:[{qui, role, principal}]}`. Le champ `role` est du texte libre repris de l'acte — « gendre déclarant », « témoin, voisin », « mère présente et consentante ».

## 5. Marche à suivre

Procéder par étapes, **en vérifiant le rendu à chaque étape**. Ne pas tout convertir d'un coup.

**Étape 0 — filet de sécurité.** Copier le fichier actuel en `arbre-…-v1.html` et le garder tel quel jusqu'à validation finale. C'est la référence de comparaison visuelle.

**Étape 1 — extraire les données sans rien changer au rendu.** Écrire un script d'extraction jetable (Python, dans `outils/`, non publié) qui lit le HTML actuel et produit les trois tableaux : 30 fiches avec leurs `--x/--y/--w`, 9 unions, et les actes déduits des `.acts` et des 62 transcriptions. **Relire le résultat à la main** : l'extraction ne saura pas lire les nuances (un `<i>` qui porte une réserve, un `?` qui qualifie la date et non le lieu). Le tableau extrait est un brouillon, pas une vérité.

**Étape 2 — brancher le moteur.** Reprendre le JS de `proto.html` tel quel, l'alimenter avec les données réelles, et comparer côte à côte avec `v1.html`. Les fils générés doivent tomber au même endroit que les 26 tracés manuels, à quelques pixels près. Là où ils diffèrent, c'est presque toujours le moteur qui a raison et le tracé manuel qui avait été bricolé.

**Étape 3 — cas particuliers.** Yvonne (trois filiations), Joséphine (deux mariages, deux pastilles sur la même ligne), le remariage de François AMIOT, l'union « possible » de 1930, la fratrie PAUFARD des douze enfants (aujourd'hui un encart, pas des fiches — la garder en encart pour l'instant, mais l'alimenter depuis les données).

**Étape 4 — tiroir et actes.** Porter les récits : le contenu existe déjà, dispersé entre `note-line`, encarts et gloses. Chaque phrase doit retrouver sa place — `recit` pour la narration, `notes` pour les réserves, `mentions` pour les rôles dans les actes. C'est l'étape la plus longue et celle où l'on perd de l'information si on va vite.

**Étape 5 — parenté, modes, frise, liens profonds.** Point de vue par défaut : la personne la plus jeune de la génération VII. Vérifier les libellés produits sur une dizaine de couples avant de publier — le calcul dit « cousin germain de son grand-père Louis » et non « au 4ᵉ degré », c'est voulu.

**Étape 6 — recette.** Voir § 6.

## 6. Recette avant publication

- [ ] Les 30 personnes, 9 unions et 62 transcriptions sont toutes présentes ; aucun texte perdu. Comparer les comptes avec `v1.html`.
- [ ] `?audit` ne signale **aucun** chevauchement.
- [ ] Aucune fiche tronquée : toutes les fiches ont `min-height`, jamais `height` fixe avec `overflow:hidden`.
- [ ] Les tracés arrivent bien sur les bords des fiches, les pastilles sont centrées sur le trait de mariage.
- [ ] Les pointillés rouges sont aux mêmes endroits qu'avant : mêmes fiches douteuses, mêmes unions probables.
- [ ] Le code documentaire (`a-n`/`a-m`/`a-d`/`a-x`) donne le même compte d'actes en main qu'avant, personne par personne.
- [ ] Surbrillance : cliquer sur François AMIOT allume toute la descendance jusqu'à la génération VII et **n'allume pas** les branches PAUFARD collatérales ; cliquer sur Yvonne en mode *Ancêtres* remonte par sa filiation biologique.
- [ ] Un acte cliqué dans le tiroir ouvre la bonne transcription ; chaque transcription renvoie aux personnes nommées.
- [ ] Impression : l'arbre tient encore sur une page A3 paysage, le dossier suit.
- [ ] Ouverture depuis un téléphone : lisible, glissement horizontal fonctionnel, tiroir en feuille basse.
- [ ] Fichier ouvert **hors connexion** : rien ne casse.

## 7. Pièges connus

- **Ne pas laisser un placement automatique s'installer.** Tentant, et destructeur : la composition actuelle dit quelque chose (les branches collatérales à gauche, la ligne directe au centre). Les `x/y` restent écrits à la main.
- **`layout()` mesure le DOM** : il doit tourner après le chargement des polices, sinon les hauteurs sont fausses. Le proto le rappelle sur `window.load`.
- **Les hauteurs `--h` sont des minima.** Ne jamais revenir à une hauteur fixe pour « aligner » une rangée.
- **Les identifiants sont publics** : ils apparaissent dans les URL partagées à la famille. Les choisir stables et lisibles, ne jamais les renommer après publication.
- **Ne pas convertir les `footnotes` et le `dossier` en données** à cette étape. Ce sont des textes éditoriaux, pas des enregistrements ; leur tour viendra peut-être, il n'est pas venu.
- **Les extensions du § 4 n'existent pas dans le proto** — le proto suppose un seul couple de parents par personne, et le dit. C'est le premier endroit où il faudra écrire du code neuf.
- **Séparer les données du moteur** (`donnees.js` + `index.html`) est prévu mais **pas dans cette étape** : le fichier unique reste la cible tant que la conversion n'est pas validée. Ne pas anticiper.

## 8. Après chaque séance de dépouillement

Une fois la conversion faite, la routine devient : éditer `ACTES` et `PERSONNES`, marquer `neuf:true` sur les apports, mettre à jour le badge de date et la mention de séance en tête, ajouter la ou les transcriptions, compléter les pistes de recherche, passer `?audit`, commiter.

---

## 9. État — conversion faite

Les six étapes sont passées. `index.html` se régénère à partir de ses données ; il reste
un fichier unique, sans dépendance, sans stockage navigateur, qui s'ouvre au double-clic.

`outils/verifier.py` tient la recette du § 6 : 60 contrôles, aucun écart.

Ce que la conversion a appris sur le document d'origine, et qui vaut d'être noté :

- **quinze fiches sur trente débordaient déjà leur `--h` déclaré**, jusqu'à 108 px. Les
  fils avaient été tracés sur la hauteur déclarée : ils n'atteignaient pas le vrai bord
  des fiches. Le moteur, qui mesure le DOM, les y ramène ;
- les **deux chevauchements** que signalait `?audit` préexistaient. L'allègement des
  fiches les a fait disparaître ;
- le **code documentaire d'une fiche dit « acte en notre possession »**, et les
  transcriptions n'en sont qu'une partie : les deux inventaires divergent légitimement ;
- l'**appariement automatique des actes aux personnes est un piège** : il attribuait à
  Joséphine († 1905) un décès de 1879 qui est celui d'une homonyme collatérale. La table
  `SUJETS` d'`outils/actes.py` est écrite à la main pour cette raison ;
- **un âge ne se calcule pas en soustrayant deux millésimes.** Yvonne, née le 1ᵉʳ octobre
  1889 et morte le 11 février 1963, a 73 ans et non 74.

Les scripts d'`outils/` ont fait leur office et sont à supprimer avec `v1.html` et le mode
`?calque` une fois la conversion validée. La routine d'après séance redevient celle du
§ 8, à ceci près qu'on édite désormais les tableaux du bas de `index.html` et non plus
des coordonnées.
