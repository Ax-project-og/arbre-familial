# CLAUDE.md

Contexte permanent du projet. À lire avant toute modification.

## 1. Ce qu'est ce dépôt

Un **arbre généalogique de la branche maternelle**, publié en page web statique sur GitHub Pages pour être consulté par la famille. Ce n'est pas une application : c'est un **document éditorial** — un dossier de recherche mis en forme, qui se lit comme un article et se met à jour après chaque séance de dépouillement aux archives.

Fichiers :

| Fichier | Rôle |
|---|---|
| `index.html` | **Le document réel.** Fichier unique, HTML + CSS + JS, aucune dépendance externe. C'est ce qui est publié. |
| `proto.html` | **Maquette d'architecture** avec des données fictives. Sert de modèle pour la version interactive à venir. Ne contient aucune donnée réelle. |
| `CONVERSION.md` | Le plan de migration du document réel vers le modèle de `proto.html`. |
| `arbre-branche-maternelle-v1.html` | **Temporaire.** Copie du document d'avant conversion, référence de comparaison visuelle. À supprimer une fois la conversion validée. |
| `outils/` | **Non publié, jetable.** Scripts d'accompagnement de la conversion : `extraire.py`, `convertir.py`, `verifier.py`, le moteur `moteur.js` et les données extraites. À supprimer avec `v1.html`. |

Le document réel fait ~5 200 lignes et ~435 Ko. Il n'y a **ni build, ni bundler, ni npm, ni framework**. On ouvre le fichier dans un navigateur, ça marche. Cette contrainte est délibérée : la famille doit pouvoir l'ouvrir dans dix ans, et le dépôt doit rester lisible dans un diff GitHub.

Les scripts d'`outils/` ne font pas exception : ce ne sont pas des étapes de construction,
mais l'échafaudage de la conversion. **Elle est faite : `index.html` s'édite maintenant
directement**, et `outils/convertir.py` est verrouillé — le relancer reconstruirait le
fichier depuis `v1.html` et effacerait tout ce qui a été fait depuis. Seul
`outils/verifier.py` garde un usage : c'est la recette, et elle lit les données du
fichier publié.

## 2. La famille, en une page

Cinq lieux principaux : **Vars**, **Mont-le-Frânois**, **Champlitte**, **Fahy-lès-Autrey**, **Oyrières** (Haute-Saône), puis **Gray**, **Autrey-lès-Gray**, et deux incursions extérieures — **Lyon** (1889-1897), **Selongey** en Côte-d'Or (branche VILLETTE), **Baume-les-Dames** et **Bourges** (branche CARPENTIER).

Neuf générations numérotées **−2, −1, 0, I à VII**, d'environ 1710 à aujourd'hui. La ligne directe passe par :

AMIOT (Mont-le-Frânois) → AMIOT × RENEVIER (Vars, 1803) → PAUFARD × AMIOT (Fahy, 1836) → GRILLOT × PAUFARD (1866) → **Joséphine GRILLOT** → **Yvonne** (Lyon, 1889) → VILLETTE × GRILLOT (1906) → RIBAUT × VILLETTE (1930) → FONTANA × RIBAUT (1963) → génération VII.

Trois nœuds compliqués, qui expliquent la plupart des choix de modélisation :

- **Yvonne Marguerite GRILLOT** (1889-1963) est née fille naturelle à Lyon. Son père, Victor CARPENTIER, l'a reconnue en 1892 ; le tribunal civil de Beaune a **annulé la reconnaissance en 1897** (enfant adultérine, art. 335 du Code civil). Elle est ensuite **adoptée par sa grand-mère** Théolinde PAUFARD. Elle a donc trois filiations successives et juridiquement distinctes. Aucun modèle de données ne doit la réduire à « fille de X et Y ».
- **Joséphine GRILLOT** a **deux mariages** (CARPENTIER 1892, BOURDEAU 1899).
- **François AMIOT** s'est **remarié** après 1818 à une Françoise dont le patronyme reste douteux ; cette seconde union n'a pas de fiche.

## 3. Les conventions du document — à ne jamais casser

Ces conventions portent du sens. Les modifier silencieusement fausse la lecture du dossier.

**Fiabilité.** Trait plein = information établie ou fortement probable. **Trait pointillé rouge** (`.is-doubt`, `.aside--doubt`, `.wire--doubt`) = information incertaine, à confirmer. Le `<span class="q">?</span>` marque une donnée précise à vérifier. Le `≈` marque une date approximative. Ces marques sont *documentaires* : ne jamais recolorer une bordure pour un effet visuel, sous peine d'ambiguïté.

**Code documentaire** — les carrés colorés `.acts li` :

| Classe | Sens | Couleur |
|---|---|---|
| `a-n` | acte de naissance / baptême en main | vert `--act-n` |
| `a-m` | acte de mariage en main | bleu `--act-m` |
| `a-d` | acte de décès en main | violet `--act-d` |
| `a-x` | acte non retrouvé ou non renseigné | contour pointillé rouge |

**Apports récents.** `<span class="tag-new">…</span>` signale ce qu'a apporté la dernière séance : *Nouveau, Daté, Datée, Confirmée, Complétée, Corrigé, Prouvé, Identifié, Résolu, À trancher, Lieu, Prénom, Acte, Acte trouvé*. Le badge de date en légende (`23-25 août 2026`) et la mention de séance en tête — « quinzième séance » à ce jour — se mettent à jour à chaque séance.

**Chips de transcription** — `.chip` dans le `<p class="ref">` : nature de l'acte (`c-n`, `c-m`, `c-d`) puis qualificatifs (*Filiation*, *Cliché pâle*, *Homonyme à écarter*, `c-warn` pour les alertes).

**Typographie.** Serif (`--serif`) pour tout ce qui est contenu généalogique ; sans-serif pour les étiquettes, en petites capitales espacées. Patronymes en `<b>` majuscules, prénoms en romain. Guillemets français « … ». Dates en `JJ/MM/AAAA` dans les fiches, en toutes lettres dans les transcriptions. Heures en `17 h 30`.

## 4. Structure du document réel

`index.html` fait ~5 200 lignes, réparties ainsi — les bornes bougent à chaque
séance, se repérer plutôt sur les repères en gras :

| Lignes | Quoi | Y touche-t-on ? |
|---|---|---|
| 7-603 | l'apparence (CSS) | rarement |
| 608-621 | titre, chapeau, onglets | badge de séance, compteurs |
| 623-691 | la scène : un `<svg>` vide, rien d'autre | jamais |
| 692-816 | le dossier : les douze encarts, en HTML | **oui**, en HTML |
| 817-849 | le bas de page de l'onglet Arbre | rarement — voir plus bas |
| 851-882 | les panneaux Frise et **Recherches**, vides : le moteur les remplit | jamais |
| 885-1912 | les 71 transcriptions, en HTML | **oui**, en HTML |
| **1937-3750** | **les données** | **oui — c'est ici que tout se passe** |
| 3753-fin | le moteur, puis la vue (zoom, glissement, onglets) | jamais |

Quatre onglets : **Arbre · Frise · Recherches · Transcriptions**.

⚠️ Le bas de page de l'onglet Arbre porte **« Questions encore ouvertes »**, qui est
**produit par le moteur** (`renderOuvertes()`) à partir des recherches de priorité `P1`.
Ne rien y écrire à la main : c'est précisément ce que la refonte du § 9 a supprimé, et
`verifier.py` échoue si un `<li>` réapparaît dans la source. Les deux colonnes voisines
— patronyme, âges déclarés, homonymes, réserves de lecture, où chercher — restent, elles,
du HTML écrit à la main.

**Avant / maintenant.** Le document était écrit à la main : chaque personne existait
deux fois et sans lien — sa fiche en HTML à une position fixe, et le trait la reliant à
ses parents écrit à part en coordonnées littérales (`M845 1972 V2252 H705 V2277`).
Ajouter quelqu'un obligeait à recalculer les tracés voisins un par un, et le coût
grandissait avec l'arbre.

Aujourd'hui, deux couches. **Les données** — `PERSONNES` (30), `UNIONS` (13),
`FILIATIONS`, `UNIONS_HORS_ARBRE`, `ENCARTS`, `ACTES` (75), `GENERATIONS` (10),
`DOSSIERS` (7), `RECHERCHES` (95), `SEANCES` (4) — et **le moteur** qui les lit. `renderCards()` fabrique les fiches, `renderEncarts()` les
encarts de la scène, puis `layout()` mesure ce qui est réellement posé
(`offsetLeft/offsetTop/offsetHeight`) et en déduit fils, pastilles, losanges, bandes et
rails. **On n'écrit plus un seul tracé.** Le coût d'un ajout ne dépend plus de la taille
de l'arbre.

Les **transcriptions n'existent qu'en HTML**, dans leur onglet : il n'y a pas de tableau
`TRANSCRIPTIONS` — le doublon dormant hérité de la conversion a été supprimé. Le lien
passe par le champ `tr` de chaque acte, et `verifier.py` vérifie qu'aucun `tr` ne pointe
dans le vide et que les deux comptes s'égalent. **Un acte transcrit = une entrée `ACTES`
portant son `tr` = un `<article class="tr" id="…">`**, ni plus ni moins.

**Une personne** porte `naissance`, `deces`, `metiers[]`, `lieux[]` — et `divers[]` pour
les rubriques qui n'entrent dans aucun de ces moules (*Variantes*, *Rang*, *Parents*,
*Statut*, *En 1889*…). Rien n'est jeté : ce qui ne se structure pas se conserve tel quel.

**Un acte n'appartient à personne** : il en nomme plusieurs, chacune à un titre.
`mentions[{qui, role, principal}]` — d'où « son dossier » d'un côté, « apparaît aussi
dans » de l'autre. Attention : le code documentaire d'une fiche dit *acte en notre
possession*, et les transcriptions n'en sont qu'une partie. Un acte détenu mais non
transcrit est normal ; l'inverse aussi.

**La fiche annonce, le tiroir raconte.** La fiche ne garde que naissance, métier,
conjoint, décès. Un clic ouvre le tiroir : chronologie déduite des données, filiations,
réserves, autres mentions, unions sans fiche, dossier d'actes cliquables, parenté.

**Trois marques de doute, et une seule à la fois.** `incertain` pose le `?` sur la date,
`lieuIncertain` sur le lieu, `ageIncertain` sur l'âge déclaré ; `approx` dit qu'une date
est une fourchette. Elles ne sont pas interchangeables : Cécile FONTANA est née le
8 mars 1966, c'est le *lieu* qui porte le `?`. La frise ne hachure une vie que si ce sont
ses **dates** qui flottent.

**Parenté relative.** Un sélecteur choisit le point de vue — par défaut la plus jeune de
la génération VII — et chaque fiche annonce ce que la personne est pour lui. Au-delà de
l'arrière-grand-père, la chaîne des « arrière- » cesse d'être lisible : le calcul passe
aux mots français (*trisaïeul*, *quadrisaïeul*, … *septaïeul*), puis à « aïeul à la Nᵉ
génération ». Le calcul suit la filiation **biologique** : Victor CARPENTIER est « époux
de son arrière-arrière-grand-mère », pas son aïeul — sa reconnaissance a été annulée.

**Trois modes d'affichage.** *Arbre*, *Preuves* (la jauge documentaire apparaît, et les
fiches sans aucun acte pâlissent : ce sont les chantiers ouverts), *Nouveautés* (n'allume
que ce qu'ont apporté les dernières séances). Une recherche filtre sur nom, lieu, métier.

**La frise** (onglet à part) donne une barre par vie. Elle ne prête à personne une vie
qu'aucun acte n'atteste : quand la mort est inconnue, la barre s'arrête à la dernière
trace et s'y efface ; `vivant:true` la fait courir jusqu'à l'année en cours.

**Les âges se calculent sur les dates complètes**, jamais par soustraction de millésimes :
Yvonne, née le 1ᵉʳ octobre 1889 et morte le 11 février 1963, a 73 ans et non 74. Quand une
date est incomplète, l'âge s'annonce avec `≈` ; et un âge calculé ne vient **jamais**
doubler ni contredire un âge porté par un acte.

**Système de coordonnées.** La scène fait 1 760 px de large. Chaque personne porte `x`,
`y`, `w`, `h` ; le CSS en fait `left/top/width/min-height`. `h` est un **minimum** :
une fiche s'agrandit si son contenu déborde, et **la moitié des fiches débordent
effectivement** — les fils s'attachent au bord réel, pas au bord déclaré. Les positions
restent écrites à la main : la composition est éditoriale, un placement automatique
ferait un arbre correct et sans point de vue.

Trois réglages restent explicites dans les données, parce qu'ils relèvent de la
composition et non du calcul : `pw` (largeur d'une pastille), `bus` (hauteur du coude
d'une descente, reprise du tracé manuel — la retirer laisse le moteur la placer à
mi-chemin) et `encart` (le fil fin vers l'encart de la fratrie).

**Surbrillance de lignée.** Un clic sur une fiche allume sa descendance en bronze, son
ascendance en vert-de-gris, les conjoints entrés par alliance en anneau pâle, et estompe
le reste. `Échap` ou un second clic éteint. Les bordures gardent leur sens documentaire :
la lumière passe par un anneau et un fond teinté, jamais par la couleur du trait.

Deux modes dans l'URL : `?audit` entoure de rouge toute boîte qui en chevauche une autre
et liste les collisions en console — à utiliser après chaque ajout de contenu ; `?calque`
superpose en rouge les 26 tracés du document manuel, pour comparer. Ce dernier disparaîtra
avec la fin de la conversion.

**L'onglet Recherches** est le dossier d'enquête, sorti de la page Arbre où il avait
débordé la généalogie. Il est produit par `renderRecherches()` à partir d'un **seul
tableau**, `RECHERCHES`, dont il tire **quatre vues** : *à rechercher* (statuts `afaire`
et `encours`, groupés par dossier et triés par priorité), *négatives et pistes écartées*,
*résolues*, et le *journal des séances*. Une recherche qui aboutit change de `statut` et
passe d'elle-même d'une vue à l'autre — **aucune liste ne peut diverger d'une autre**,
puisqu'il n'y en a qu'une.

Chaque entrée porte `id`, `dossier`, `priorite` (`P1`|`P2`|`P3`|absent), `statut`,
`titre`, `ou`, `pourquoi`, et selon le cas `resultat`, `consequence`, `piece`, `seances`.
Trois règles que la recette fait respecter :

- **`negative` et `caduque` ne se confondent pas.** Avoir cherché sans rien trouver est un
  *résultat* qui contraint la suite ; constater qu'une piste n'a plus d'objet est un
  *abandon*. Les confondre fait perdre de l'information.
- **`consequence` est obligatoire** sur toute entrée `negative` ou `caduque`. Une recherche
  négative correctement rédigée ne dit pas « rien trouvé » : elle dit ce que l'échec permet
  de conclure.
- **Pas d'émoji.** Les statuts et priorités passent par les pastilles et étiquettes déjà
  définies dans la feuille de style. La sobriété typographique est un des points forts du
  rendu.

`piece` désigne un `id` d'`ACTES`, et le renvoi « Lire la pièce → » réutilise
`versTranscription()`. Les **fronts A à E et les rangs 1 à 5 sont abandonnés** : c'était un
artefact de la manière dont le dossier a grossi, pas un classement. `verifier.py` échoue si
l'un d'eux reparaît dans le document.

## 4 bis. Ce que le moteur déduit, et ce qu'il faut lui dire

La distinction commande tout le travail d'édition. **Le moteur raisonne sur un graphe
déclaré ; il ne lit aucune prose.**

**Déduit — ne jamais l'écrire à la main :**

- les **quatre vues** de l'onglet Recherches et le bloc « Questions encore ouvertes »
  de la page Arbre, entièrement tirés de `RECHERCHES` ;
- les **fils**, leur coude, les pastilles de mariage, les losanges d'union sans date ;
- les **bandes** de génération, la colonne des chiffres romains, la hauteur de la scène ;
- la **hauteur réelle** de chaque fiche, donc l'endroit exact où les fils s'y attachent ;
- l'**ascendance et la descendance** complètes de n'importe qui, à n'importe quelle
  profondeur, et la **surbrillance** qui en découle ;
- la **parenté entre deux personnes quelconques** — « époux de son arrière-arrière-
  grand-mère » n'est écrit nulle part, il se calcule sur cinq générations ;
- la **chronologie** du tiroir : naissance, domiciles, métiers, mariages, naissances des
  enfants, décès, remis dans l'ordre, avec l'âge à chaque étape ;
- la **frise**, la **jauge documentaire** du mode *Preuves*, le mode *Nouveautés*.

**Déclaré — le moteur ne le devinera jamais :**

- **qui est enfant de qui.** `enfants:[…]` dans une union, ou une entrée `FILIATIONS`.
  C'est la seule chose qui fait exister un lien ;
- **la position** `x`/`y` d'une fiche. Volontaire : la composition dit quelque chose
  (collatéraux à gauche, ligne directe au centre) qu'un placement automatique détruirait ;
- **qui figure dans quel acte** — la table `mentions` d'`ACTES`. Elle a été écrite à la
  main, et il le fallait : l'appariement automatique attribuait à Joséphine († 1905) un
  décès de 1879 qui est celui d'une homonyme collatérale, et rattachait à Jean Émile
  VILLETTE (né en 1911) un acte de 1877. **Ne jamais automatiser ce rattachement** ;
- **les rôles** dans un acte (« gendre déclarant ») : ils demandent la lecture de la pièce ;
- **toute la prose** — gloses, encarts, réserves, anecdotes, recherches négatives. Le
  moteur l'affiche, il ne la comprend pas.

En un mot : il est intelligent sur la **structure**, aveugle au **texte**. Il ne saura
jamais que le « pharmacien » du recensement de Serrigny est Carpentier tant qu'on ne
l'aura pas écrit dans `mentions`.

## 4 ter. Ajouter quelqu'un

1. Copier un bloc de `PERSONNES` voisin, changer `id`, `prenoms`, `nom`, `f`, `gen`,
   les dates. L'`id` se compose du prénom d'usage, du patronyme et de l'année de
   naissance — **il est public et définitif** dès qu'il circule dans un lien `#p=`.
2. Ajouter cet `id` aux `enfants` de l'union de ses parents. C'est ce geste, et lui seul,
   qui trace le fil.
3. Poser un `x`/`y` plausible, ouvrir le fichier, ajuster. **`?audit` dans l'URL** entoure
   de rouge toute boîte qui en chevauche une autre.
4. `outils/verifier.py` après la séance : il dit si un compte a bougé sans raison.

Un `id` cité mais inexistant fait échouer le rendu — c'est voulu, l'incohérence se voit
tout de suite. Une page blanche après une modification, c'est presque toujours une
virgule ou une accolade : `Ctrl+Maj+J` donne la ligne.

## 5. Règles de travail

**Ne jamais inventer une donnée.** Ce dossier est une enquête : chaque affirmation vient d'un acte, d'un recensement ou d'un papier de famille, et une date fausse peut envoyer quelqu'un chercher pendant des mois au mauvais endroit. Si une information manque, elle reste absente ou marquée `?`. Si une lecture est douteuse, elle est écrite entre crochets avec un point d'interrogation : `[Véroille ?]`.

**Ne jamais promouvoir une hypothèse en fait.** Les encarts distinguent explicitement ce qui est *prouvé*, *probable*, *hypothétique* et *à trancher*. Une reformulation qui gomme cette gradation est une régression, même si le texte est plus fluide.

**Ne jamais supprimer une réserve de lecture** ni une piste de recherche sans que le propriétaire l'ait explicitement demandé. Les « recherches négatives » (ce qu'on a cherché sans trouver) ont autant de valeur que les trouvailles : elles évitent de refaire le travail.

**Distinguer les sources.** Acte d'état civil > recensement > papier de famille > tradition orale. Une date venue d'une fiche manuscrite familiale se signale comme telle (« d'après les papiers de famille ») et n'efface pas une date d'acte.

**Le ton.** Prose française soignée, à la troisième personne, sans emphase inutile. Les gloses (`.gloss`) après chaque transcription expliquent *ce que la pièce apporte*, pas ce qu'elle contient — elles raisonnent. Ne pas les transformer en résumés.

**Personnes vivantes.** Les générations VI à VIII concernent des vivants. Pas d'adresses, pas d'informations sensibles ; dates de naissance et unions seulement, telles que la famille les a fournies.

## 6. Ce qui est en cours

La conversion vers un arbre interactif, décrite dans `CONVERSION.md`. `proto.html` en est la maquette validée.

**Faites** — les six étapes de `CONVERSION.md`. Le document se régénère à partir de ses
données sans perte de texte : `outils/verifier.py` passe **108 contrôles**, dont le
décompte des étiquettes d'apport rubrique par rubrique, l'absence de chevauchement,
l'absence de dépendance externe et de stockage navigateur, et — depuis la refonte du § 9 —
la cohérence de `RECHERCHES` : nomenclature des statuts et des priorités, dossiers
existants, pièces transcrites, conséquence présente sur chaque recherche négative.

Les **écarts volontaires** avec le document d'avant conversion sont inscrits dans le
dictionnaire `EVOLUTIONS`, en tête de `verifier.py`, avec leur raison : c'est ce qui permet
à une divergence *non prévue* de continuer à faire échouer la recette. Toute correction
apportée au dossier qui change un décompte doit y être consignée, jamais contournée.

Les trois nœuds compliqués du § 2 sont modélisés : les **trois filiations d'Yvonne**
(naturelle, reconnaissance annulée 1892-1897, adoptive) se lisent dans son tiroir, dans
l'ordre, tandis que le fil de l'arbre suit la biologique ; les **deux mariages de
Joséphine** partagent une ligne, parce que toutes les unions d'une personne qui s'est
mariée plusieurs fois s'alignent sur son propre centre ; le **remariage de François
AMIOT** est dans `UNIONS_HORS_ARBRE`, avec la première union de Victor CARPENTIER.

**À faire avant publication** — la recette technique passe, mais trois choses relèvent du
propriétaire du dossier :

- **relire les libellés de parenté** sur une dizaine de couples. Le calcul est vérifié,
  le vocabulaire est un choix : *septaïeul* est exact mais peu courant.
- **confirmer les identifiants**, publics et définitifs dès qu'ils circulent en `#p=`.
- **essayer sur un téléphone.** Le tiroir passe en feuille basse sous 900 px et le
  glissement horizontal fonctionne, mais cela n'a pas été vu sur un vrai appareil.

Puis, une fois validé : supprimer `arbre-branche-maternelle-v1.html`, le dossier
`outils/` et le mode `?calque`, qui n'ont plus d'objet.

**Le travail qui reste dans les données**, et qu'aucun script ne fera :

- les **rôles** dans les actes — « gendre déclarant », « témoin, voisin ». `ACTES` sait
  qui chaque acte nomme, pas à quel titre : cela demande la lecture de chaque pièce.
- le **récit** de chaque personne. Le tiroir n'en affiche pas : il n'y a pas de `recit`
  dans les données, et il n'était pas question d'en écrire un à partir de rien.
- les **identifiants**, publics et définitifs dès qu'ils circulent en `#p=`. Quatre
  suivent le nom d'usage du dossier plutôt que le premier prénom : `theolinde-`,
  `josephine-`, `napoleon-`, `claude-alexis-`. À confirmer avant publication.
- les **dates non structurées** : celles que l'extraction n'a pas su lire sans risque de
  contresens sont restées absentes plutôt que devinées. Voir
  `outils/rapport-extraction.md`.
