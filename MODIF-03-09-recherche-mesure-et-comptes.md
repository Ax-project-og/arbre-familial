# ARBRE GÉNÉALOGIQUE — BRANCHE MATERNELLE
# MODIF 03/09 — La recherche, la mesure de l'arbre, et les comptes qui ont dérivé

*Aucun acte nouveau · Un défaut fonctionnel · Une régression de mise en page · Quatre endroits où le nombre de maisons GRILLOT ne dit pas la même chose · Deux détails*

---

## 0. Contexte — ce que fait ce patch, et ce qu'il ne fait pas

Claude, **ce patch n'apporte aucune donnée nouvelle**. Aucune personne à créer, aucune union, aucune transcription. C'est un patch de relecture, passé sur la refonte visuelle : il répare un défaut fonctionnel, une régression de mise en page, et une dérive de chiffres qui s'est installée entre la seizième et la dix-huitième séance.

**Le défaut fonctionnel (§1).** Le champ de recherche de l'en-tête collant a l'air global — il est dans le bandeau, il est présent sur les six onglets — mais `filtrerPanneau()` ne travaille que sur une liste fermée de cibles, et cette liste ne couvre pas l'onglet **Le dossier**. Résultat concret : on ouvre Le dossier, on tape « REDOUTET », et le décompte répond *rien à filtrer ici* alors que le nom est affiché six fois à l'écran. C'est le panneau le plus dense du site — quinze encadrés, tous les collatéraux — et c'est le seul où chercher un nom ne donne rien. Au passage, une des cibles de la liste, `.note-marge`, est **stylée mais jamais émise** : aucun élément du document ne porte cette classe.

**La régression de mise en page (§2).** L'onglet Arbre a été enveloppé dans `<div class="wrap">` comme les autres, donc plafonné à `--max` (1 240 px). Avec les 32 px de marge de la mesure et les 18 px de padding du `#viewport`, il reste environ 1 140 px utiles pour une scène large de **1 760 px**, et `echelleDepart()` renvoie 1 au-dessus de 760 px de viewport : sur un écran de bureau, l'arbre s'ouvre donc à taille réelle dans une fenêtre qui en montre les deux tiers, et il faut le tirer à la main. Dans la version précédente `.sheet` montait à 1 820 px et l'arbre tenait entier. La mesure de 1 240 px est excellente pour tous les autres panneaux ; c'est l'arbre, et lui seul, qui doit en sortir.

**La dérive des comptes (§3 et §4).** La seizième séance avait établi **quatre** maisons GRILLOT à Gray ; la dix-huitième en a ajouté quatre autres, et le titre de l'encadré a été porté à **huit**. Mais la correction n'a pas été passée partout. Le document dit aujourd'hui *quatre*, *sept* et *huit* selon l'endroit où on le lit, et le paragraphe « Ce qui reste ouvert » de la synthèse annonce encore les décès de Jacques et de Joseph comme devant dire « si les **quatre** maisons de Gray n'en font qu'une », quatre lignes sous un paragraphe qui en compte huit. Il manque par ailleurs, dans la même synthèse, le paragraphe de la **dix-septième séance** : elle existe dans `SEANCES`, elle a livré le mariage de Marnay, et la synthèse saute de la seizième à la dix-huitième. Ses trouvailles sont bien là, mais rangées **dans le paragraphe « Ce qui reste ouvert »**, ce qui est le mauvais endroit : ce sont des acquis, pas des questions.

**Principe de rédaction à retenir pour la suite**, parce que c'est la troisième fois que ce type de dérive apparaît : partout où c'est possible sans perte de sens, **préférer une formulation sans chiffre** (« ces maisons ») à une formulation chiffrée (« les quatre maisons »). Un chiffre écrit à la main dans un texte narratif est une promesse qu'il faudra tenir à chaque séance.

---

## 1. La recherche globale doit atteindre l'onglet Le dossier

### 1.1 — La liste des cibles

Fichier `index.html`, section 10 du JS. Remplacer :

```js
const CIBLES_FILTRE = '.branche, .pistes > li, .rq, .tr-liste li:not(.grp), .note-marge, .ca-loin li';
```

par :

```js
/* Les unités que le champ de l'en-tête peut montrer ou cacher. Elles doivent
   couvrir chaque panneau, faute de quoi la recherche répond « rien à filtrer
   ici » sur un panneau plein de texte — c'était le cas du Dossier, dont les
   quinze encadrés n'étaient atteints par aucune de ces cibles. `.note-marge`
   a été retirée : la classe est stylée mais aucun élément ne la porte. */
const CIBLES_FILTRE = '.branche, .pistes > li, .rq, .tr-liste li:not(.grp), '
                    + '.aside .roster > li, .aside .unions > li, .ca-loin li';
```

### 1.2 — Ne pas laisser un encadré vide à l'écran

Un encadré dont toutes les lignes sont filtrées resterait affiché avec son seul titre, ce qui est pire que rien. Dans `filtrerPanneau()`, deux ajouts.

**a)** Dans la remise à zéro, juste après la ligne existante :

```js
  document.querySelectorAll(CIBLES_FILTRE).forEach(x => x.classList.remove('hors-jeu'));
```

ajouter :

```js
  document.querySelectorAll('.aside.hors-jeu').forEach(x => x.classList.remove('hors-jeu'));
```

C'est indispensable : `.aside` n'est pas dans `CIBLES_FILTRE`, donc la ligne au-dessus ne le rallumerait jamais.

**b)** À la fin de la branche générique — après la boucle `items.forEach(...)` et **avant** l'écriture de `dec.textContent` :

```js
  /* Un encadré dont toutes les lignes sont filtrées ne doit pas rester à
     l'écran réduit à son titre. On n'éteint que ceux qui ont des lignes :
     un encadré sans liste n'est pas concerné. */
  if (pan) pan.querySelectorAll('.aside').forEach(a => {
    const lignes = [].slice.call(a.querySelectorAll('.roster > li, .unions > li'));
    a.classList.toggle('hors-jeu',
      lignes.length > 0 && !lignes.some(x => !x.classList.contains('hors-jeu')));
  });
```

### 1.3 — Vérification attendue

Sur l'onglet **Le dossier**, taper `REDOUTET` doit laisser visibles les lignes des encadrés « Les PAUFARD de Fahy » et « Collatéraux relevés dans les actes », éteindre les autres encadrés entièrement, et afficher un décompte non nul. Taper `GACONNET`, `BERNARDOT`, `THURIET` doit donner un résultat chacun. Vider le champ doit tout rallumer, encadrés compris.

---

## 2. L'arbre sort de la mesure de lecture

### 2.1 — CSS

Ajouter, à côté de la définition de `.wrap` (section 2, Fondations) :

```css
/* L'arbre est la seule pièce du document qui ne se lise pas en colonne :
   la scène fait 1 760 px et doit tenir dans la fenêtre sans qu'on la tire
   à la main. Elle sort donc de la mesure de lecture, que les autres
   panneaux gardent. 1 880 = 1 760 + les marges de .wrap + le padding
   de #viewport, avec un peu de jeu. */
.wrap--large{max-width:1880px}
```

### 2.2 — HTML

Dans `#panel-arbre`, remplacer :

```html
  <section class="panel" id="panel-arbre" hidden role="tabpanel" aria-labelledby="tab-arbre">
    <div class="wrap">
```

par :

```html
  <section class="panel" id="panel-arbre" hidden role="tabpanel" aria-labelledby="tab-arbre">
    <div class="wrap wrap--large">
```

### 2.3 — Vérification attendue

Sur un écran de 1 920 px, l'arbre doit tenir entier sans panoramique et l'indication `#panHint` doit rester masquée. Sous 1 880 px, le comportement actuel reprend, ce qui est correct. Attention en relisant : `.wrap` (la classe de mesure) et `#wrap` (le conteneur de la scène, à l'intérieur de `#viewport`) sont deux choses différentes et voisines dans le même panneau — ne pas confondre les sélecteurs.

---

## 3. La synthèse du dossier — cohérence et paragraphe manquant

Tout ce qui suit est dans `#panel-dossier`, `<div class="synthese-corps">`. Les paragraphes sont séparés par `<br><br>`.

### 3.1 — Rendre au seizième paragraphe son compte d'époque

La seizième séance a établi quatre maisons, pas huit. Lui faire dire huit est une erreur de chronologie dans un texte organisé par séance. Remplacer :

```
les tables ont livré <b>huit maisons GRILLOT distinctes</b> dont une seule est la nôtre, et deux homonymes tombent.
```

par :

```
les tables ont livré <b>quatre maisons GRILLOT distinctes</b> dont une seule est la nôtre, et deux homonymes tombent — la dix-huitième séance en portera le compte à huit.
```

### 3.2 — Insérer le paragraphe de la dix-septième séance

Il manque entièrement. Ses trouvailles sont pour l'instant logées dans « Ce qui reste ouvert », d'où le §3.3 les retire. Insérer **avant** le paragraphe de la dix-huitième séance.

Remplacer :

```
<b>La dix-huitième séance ouvre la génération −1 des PAUFARD.</b>
```

par :

```
<b>La dix-septième séance ferme la génération d'avant les GRILLOT.</b> Le <b>mariage de Marnay</b>, en 1833, nomme la mère de Jeanne ÉCARNOT et date les décès de <b>Noël GRILLOT</b>, de <b>Jean Pierre ÉCARNOT</b> et de <b>Marguerite GARDOT</b> : les deux mariés étaient orphelins, et sur six ascendants un seul vivait — <b>Anne Pierre BERNARDOT, bouchère à Gray</b>, qui fait le voyage depuis Gray et signe de sa main. À Gray même, le décès de Noël en 1832 le donne <b>rue de la Varosse</b>, déclaré par un ami ; les tables de décès de 1823 à 1842 ne portent <b>ni Jacques ni Joseph</b>, et la table des naissances de 1843 à 1852 <b>aucune naissance GRILLOT en douze ans</b>. Deux recherches négatives ferment autant de portes : les <b>successions du bureau de Gray</b> ne donnent rien entre 1824 et 1944, et <b>Clotilde Hortense</b> est absente des décès de Fahy.<br><br>
      <b>La dix-huitième séance ouvre la génération −1 des PAUFARD.</b>
```

L'indentation de six espaces devant `<b>La dix-huitième…</b>` reproduit celle des autres paragraphes du bloc ; la conserver telle quelle.

### 3.3 — Réparer « Ce qui reste ouvert »

Deux choses à la fois : le compte faux, et le bloc de Marnay qui n'a rien à faire dans une liste de questions ouvertes puisqu'il est résolu. Remplacer :

```
les <b>décès de Jacques et de Joseph GRILLOT</b>, qui diraient si les quatre maisons de Gray n'en font qu'une. <b>Le mariage de Marnay</b>, en 1833, ferme cette génération : il nomme la mère de Jeanne ÉCARNOT et date les décès de <b>Noël GRILLOT</b>, de <b>Jean Pierre ÉCARNOT</b> et de <b>Marguerite GARDOT</b>. Les deux mariés étaient orphelins ; sur six ascendants, un seul vivait — <b>Anne Pierre BERNARDOT, bouchère à Gray</b>, qui fait le voyage et signe de sa main. L'onglet
```

par :

```
les <b>décès de Jacques et de Joseph GRILLOT</b>, qui diraient si ces maisons n'en font qu'une. L'onglet
```

---

## 4. Les trois autres endroits où le compte a dérivé

### 4.1 — L'encadré « Les GRILLOT de Gray »

Le titre dit *au moins huit maisons*, la liste en contient huit, mais la ligne « Le problème » en annonce sept. Remplacer :

```
Les maisons ci-dessous se lisent <b>en deux temps</b> — quatre au tournant du siècle, trois de plus dans les années 1830 — et une seule est la nôtre
```

par :

```
Les maisons ci-dessous se lisent <b>en deux temps</b> — quatre au tournant du siècle, quatre de plus dans les années 1830 — et une seule est la nôtre
```

### 4.2 — La note « Homonymes à écarter », dans `.footnotes`

Remplacer :

```
a fait apparaître <b>au moins sept foyers GRILLOT</b> distincts, quatre au tournant du siècle et trois dans les années 1830 — dont <b>un seul est le nôtre</b>.
```

par :

```
a fait apparaître <b>au moins huit foyers GRILLOT</b> distincts, quatre au tournant du siècle et quatre dans les années 1830 — dont <b>un seul est le nôtre</b>.
```

### 4.3 — L'entrée `RECHERCHES` correspondante

L'entrée est enregistrée comme résolue par la seule seizième séance, alors que la dix-huitième l'a complétée. L'identifiant `quatre-maisons-grillot-de-gray` n'est référencé nulle part ailleurs dans le fichier — je l'ai vérifié — il peut donc être renommé sans risque. Remplacer :

```js
{id:"quatre-maisons-grillot-de-gray", dossier:"grillot-paufard", statut:"resolue",
 titre:"Y a-t-il plusieurs familles GRILLOT à Gray ?",
 ou:"Tables décennales de Gray, dix décennies, puis six actes ouverts entre l'an II et l'an X.",
 pourquoi:"Une trentaine de GRILLOT entre 1792 et 1892, et aucun moyen de savoir lesquels retenir.",
 resultat:"<b>Au moins quatre maisons</b>, dont trois nommées par acte : <b>Jacques × Claudine VALLON</b> (bouchers), <b>Marie Ferréol × Jeanne Baptiste PREVOT</b> (propriétaire puis secrétaire de mairie), <b>Joseph × Anne MARCHAND</b>, et la nôtre. La démonstration est <b>arithmétique</b> avant d'être documentaire : deux naissances GRILLOT à six jours d'intervalle en décembre 1835, deux autres à quatre mois en 1826. <i>Aucune mère ne peut faire cela.</i>",
 piece:"a-1793-1802-les-deux-maisons-grillot-de-gray",
 seances:["28-29/08/2026"]},
```

par :

```js
{id:"maisons-grillot-de-gray", dossier:"grillot-paufard", statut:"resolue",
 titre:"Y a-t-il plusieurs familles GRILLOT à Gray ?",
 ou:"Tables décennales de Gray, dix décennies, puis six actes ouverts entre l'an II et l'an X ; complété par les naissances de 1833-1842.",
 pourquoi:"Une trentaine de GRILLOT entre 1792 et 1892, et aucun moyen de savoir lesquels retenir.",
 resultat:"<b>Au moins huit maisons</b>, en deux temps. Quatre au tournant du siècle : <b>Jacques × Claudine VALLON</b> (bouchers), <b>Marie Ferréol × Jeanne Baptiste PREVOT</b> (propriétaire puis secrétaire de mairie), <b>Joseph × Anne MARCHAND</b>, et la nôtre. Quatre dans les années 1830 : <b>François × Françoise THÉVENIN</b> (manouvrier), <b>Jean × Anne Baptiste LÉONARD</b> (paveur), <b>François × Anne PAGE</b>, et <b>Nicolas Louis × Anne Antoinette BAILLY</b> (charpentier) — cette dernière n'étant peut-être pas étrangère, mais un frère de Thomas. La démonstration est <b>arithmétique</b> avant d'être documentaire : deux naissances GRILLOT à six jours d'intervalle en décembre 1835, deux autres à quatre mois en 1826. <i>Aucune mère ne peut faire cela.</i>",
 piece:"a-1793-1802-les-deux-maisons-grillot-de-gray",
 seances:["28-29/08/2026","30/08/2026 · soir"]},
```

Les chaînes de `seances` doivent correspondre **exactement** aux `date` de `SEANCES`, sans quoi le journal ne rattachera pas la recherche à sa séance : `"30/08/2026 · soir"` est bien la valeur littérale de la dix-huitième.

---

## 5. Deux détails

### 5.1 — La datation ne sait pas lire une date à intervalle

`renderAccueil()` formate la date de la dernière séance avec une expression qui n'accepte que `jj/mm/aaaa`. La seizième séance est datée `28-29/08/2026` : si une séance ainsi datée redevenait la dernière, la date s'afficherait en brut au milieu de ses voisines formatées. Remplacer :

```js
    const m = /^(\d{2})\/(\d{2})\/(\d{4})/.exec(s0.date || '');
    const MOIS = ['janvier','février','mars','avril','mai','juin','juillet','août',
                  'septembre','octobre','novembre','décembre'];
    const quand = m ? (+m[1]) + ' ' + MOIS[+m[2] - 1] + ' ' + m[3] : (s0.date || '');
```

par :

```js
    /* Une séance peut courir sur deux jours — « 28-29/08/2026 ». Le quantième
       est donc lu comme une chaîne, dont on retire les zéros de tête. */
    const m = /^(\d{1,2}(?:-\d{1,2})?)\/(\d{2})\/(\d{4})/.exec(s0.date || '');
    const MOIS = ['janvier','février','mars','avril','mai','juin','juillet','août',
                  'septembre','octobre','novembre','décembre'];
    const jour = m ? m[1].split('-').map(n => String(+n)).join('-') : '';
    const quand = m ? jour + ' ' + MOIS[+m[2] - 1] + ' ' + m[3] : (s0.date || '');
```

### 5.2 — `--encre-3` n'atteint pas le seuil que le commentaire vise

Le bloc de jetons pose la règle des 4,5:1 pour les textes. `--encre-3` (#5D6C85) mesure **4,46:1** sur le parchemin — à un cheveu, mais en dessous, et c'est la couleur qui porte les libellés en capitales. Remplacer :

```css
  --encre-3:#5D6C85;
```

par :

```css
  --encre-3:#59687F;   /* 4,75:1 sur le parchemin, 5,42:1 sur la carte */
```

Vérifié : les six autres couleurs de texte de la palette passent le seuil, et `--encre-4` est bien réservée aux traits (deux usages, tous deux des bordures). Rien d'autre à toucher.

---

## 6. Ce que je n'ai pas fait, et qui attend un arbitrage

Ne rien coder ici sans retour. Je les note pour mémoire.

**Le routage par onglet dans l'URL.** Seules les personnes sont adressables (`#p=id`). Avec six onglets, une transcription ouvrable et une carte à trois échelles, ne pas pouvoir envoyer un lien vers *Le dossier* ou vers un acte précis coûte cher dès qu'on travaille à deux sur le document. Ce serait un `#onglet=…` et une reprise de `versAncre()`.

**Le doublon du filtre sur l'onglet Transcriptions.** Le champ de l'en-tête et le champ `#qActes` filtrent la même liste `.tr-liste`. Deux champs pour un seul filtre, dont l'un dans un bandeau qui prétend chercher partout. Soit on retire `.tr-filtre`, soit on donne à `#qActes` un rôle distinct — filtrer les articles eux-mêmes et non la liste latérale.

**Le triple emploi de la matière narrative.** Les six chapitres de `RECITS`, la `synthese-corps` et le journal des séances racontent la même histoire à trois endroits. Le commentaire de la section 7 du JS le dit lui-même : « faute de quoi la page d'accueil finirait par contredire le dossier — c'est déjà arrivé ». Le présent patch répare les divergences ; il ne supprime pas leur cause. À trancher : réduire la `synthese-corps` à ses deux premiers paragraphes, stables, et laisser les séances au journal.

---

## 7. Récapitulatif des fichiers touchés

Un seul fichier, `index.html`.

| § | Emplacement | Nature |
|---|---|---|
| 1.1 | JS, `CIBLES_FILTRE` | 1 ligne remplacée par 3 |
| 1.2 | JS, `filtrerPanneau()` | 2 ajouts |
| 2.1 | CSS, section 2 | 1 règle ajoutée |
| 2.2 | HTML, `#panel-arbre` | 1 attribut de classe |
| 3.1–3.3 | HTML, `.synthese-corps` | 3 remplacements de texte |
| 4.1 | HTML, encadré GRILLOT | 1 remplacement de texte |
| 4.2 | HTML, `.footnotes` | 1 remplacement de texte |
| 4.3 | JS, `RECHERCHES` | 1 entrée réécrite |
| 5.1 | JS, `renderAccueil()` | 3 lignes remplacées par 5 |
| 5.2 | CSS, `:root` | 1 valeur |

Aucune donnée généalogique n'est modifiée : ni `PERSONNES`, ni `UNIONS`, ni `SEANCES`, ni les transcriptions. Les compteurs restent à **315 personnes** et **90 actes**, calculés.
