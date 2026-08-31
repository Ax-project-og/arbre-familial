# Refonte visuelle du site généalogique — instructions

## Objet

Appliquer à `index.html` l'environnement graphique du fichier joint `proto-visuel.html`.
**Il s'agit d'une refonte purement graphique.** Le contenu généalogique du site — noms, dates,
lieux, transcriptions, fiches, pistes de recherche, notes, hypothèses — ne doit être ni réécrit,
ni résumé, ni réordonné, ni raccourci. Tout ce qui est aujourd'hui affiché doit continuer de
l'être, mot pour mot.

Deux exceptions, et deux seulement :

1. L'onglet **Frise** disparaît, remplacé par un onglet **Carte** (voir § 4).
2. Les **récits de la page d'accueil** sont fournis ci-dessous, prêts à intégrer (voir § 7).
Ils sont tirés de la synthèse déjà présente dans `index.html` — ils ne l'inventent pas,
ils la découpent.

En cas de doute sur l'emplacement d'un bloc existant, **demande plutôt que de trancher**.
Perdre une information vaut bien plus cher qu'une question.

\---

## 1\. Fichiers

|Fichier|Rôle|
|-|-|
|`index.html`|Le site. C'est lui qui est modifié.|
|`proto-visuel.html`|Le prototype graphique. Source des choix visuels. **Ne pas le livrer, ne pas le fusionner tel quel.**|

Le prototype est une maquette : ses textes sont fictifs ou schématiques, ses fiches d'arbre sont
des cartons vides, son moteur est un décor. **On lui prend son habillage, pas son contenu ni sa
logique.** Le sens de la reprise est : le contenu de `index.html` entre dans le costume du
prototype, jamais l'inverse.

\---

## 2\. Ce qui est repris du prototype

**Les jetons CSS** (bloc `:root`) : palette parchemin / encre / laiton / grenat, familles
typographiques, `--tete`, `--tiroir`, `--max`. Ils remplacent les valeurs équivalentes
d'`index.html`.

Attention à deux paires de variables, qui existent pour une raison :

* `--laiton` sert aux filets, bordures et grands chiffres ; `--laiton-txt` sert aux **textes**
(le premier ne dépasse pas 3,1:1 sur le parchemin).
* `--encre-3` sert aux textes secondaires ; `--encre-4` est réservé aux filets.

Ne pas les confondre en portant les règles, et ne pas descendre les étiquettes en capitales
sous 9,5 px : c'était le principal défaut de lisibilité du site actuel.

**Les composants**, dans l'ordre du prototype :

* en-tête collant sombre à filet de laiton, onglets, champ de recherche ;
* frontispice : datation, titre, chapeau à lettrine, cartouche « État du dossier » ;
* bande de nuit « La ligne directe » (les six alliances) ;
* le récit en page centrée (`.colonnes--pleine`, 884 px) ;
* les cartes de branches ;
* « Ce qui reste ouvert » ;
* les fiches, sceaux et vues de l'onglet Recherches ;
* la mise en page à deux colonnes des Transcriptions ;
* le tiroir latéral de fiche personne ;
* le pied de page.

**Les acquis techniques du prototype**, à ne pas perdre en cours de route : la feuille
`@media print`, le lien d'évitement, la règle `:focus-visible` unique, les rôles `tablist` /
`tabpanel` avec navigation aux flèches, le piège à focus du tiroir et la restitution du focus au
déclencheur, les points de rupture (1080 / 980 / 720 / 560) et les `minmax(0,1fr)` qui évitent le
débordement horizontal.

\---

## 3\. L'arbre

**Le moteur d'arbre actuel est conservé intégralement** : structure de données, calcul des
positions, tracé des liens, zoom, glissement horizontal, points de vue, modes d'affichage
(Arbre / Preuves / Nouveautés), impression. On ne le réécrit pas.

Ce qui change est l'habillage :

* la carte-personne prend l'apparence de `.fiche` du prototype — fond crème, filet fin,
bordure gauche épaisse (encre pour les hommes, grenat pour les femmes), bordure en tirets pour
les filiations incertaines, bordure doublée pour les têtes de branche ;
* le code documentaire (naissance / mariage / décès / non retrouvé) garde ses couleurs actuelles
et devient la rangée de pastilles en pied de fiche ;
* les nœuds d'alliance prennent la forme du prototype (losanges + millésime) ;
* la barre d'outils reprend `.barre` : légendes de fiabilité, code documentaire, point de vue,
boutons segmentés, zoom, impression ;
* les repères « Nouveau » deviennent les `.jalon` du prototype.

Un clic sur une fiche ouvre le tiroir, comme aujourd'hui.

\---

## 4\. Frise → Carte

L'onglet **Frise** est supprimé : bouton, panneau, styles et code de rendu associés.

À sa place, un onglet **Carte**, à la même position dans la barre.

Les communes qui devront y figurer, si la carte est à construire : Mont-le-Frânois, Vars,
Oyrières, Champlitte, Fahy-lès-Autrey, Autrey, Gray, Ancier, Le Magny, Champvans-lès-Dole,
Marnay, Baume-les-Dames, Trouvans, Serrigny, Beaune, Selongey, Lyon, Nancy, Dijon, Paris.

\---

## 5\. Les autres onglets

**Recherches.** Le site tient les quatre vues à partir d'un seul tableau (À rechercher,
Négatives et pistes écartées, Résolues, Journal des séances) : **cette logique est conservée**,
ainsi que les deux axes dossier thématique / priorité. Seul l'habillage change — `.sous-nav`
pour les vues, `.piste` pour les fiches, `.prio` pour les priorités, `.sceau` pour les états,
`.reponse` pour les conclusions. Le prototype n'a que trois niveaux de priorité et quatre vues :
si le site en a davantage, **c'est le site qui a raison**, ajoute les classes manquantes.

**Transcriptions.** Les quatre-vingt-six actes, leurs textes, leurs références d'archives et
leurs mentions de mots douteux passent inchangés. La note liminaire sur la modernisation de la
ponctuation et les crochets est conservée. On adopte la liste à gauche et l'acte à droite, avec
le bloc « Ce que cet acte apprend ».

**Le dossier — relevés, hypothèses, collatéraux.** Ce long bloc de l'onglet Arbre, avec ses
encadrés (« Ce que l'on ignore encore en amont », « L'année 1807 à Vars », les collatéraux, les
parrainages croisés, les points « À trancher »), **doit être intégralement conservé**. Il se
prête bien aux `.note-marge` du prototype, ou à des `.piste` si tu préfères. Si sa place te
paraît ambiguë, demande.

\---

## 6\. Le frontispice

Reprendre tel quel de `index.html` :

* « Document de travail · Recherches en cours · Mise à jour : 30 août 2026, dix-septième séance »
→ la ligne `.datation` ;
* le titre et son sous-titre ;
* le chapeau de synthèse, qui devient le `.chapo` à lettrine. Il est long : garde-le entier, ou
n'en mets en chapeau que le premier tiers et laisse le reste descendre dans les récits du § 7,
qui le reprennent déjà. **Ne le résume pas.**

Le cartouche « État du dossier » se remplit avec les compteurs réels du site : personnes,
actes transcrits (86), générations (de −2 à VII, soit 9), pistes ouvertes. S'ils sont calculés
dynamiquement, garde le calcul.

\---

## 7\. Les récits de la page d'accueil

À placer dans la section « Le récit », en six `.chapitre` successifs. La numérotation romaine est
automatique (compteur CSS) : ne pas la saisir à la main.

Ces textes sont bâtis sur les faits déjà présents dans `index.html`. Ils n'ajoutent aucune
donnée. S'ils contredisent quoi que ce soit dans le dossier, **c'est le dossier qui fait foi** —
signale-le-moi plutôt que de corriger seul.

\---

### I — Le berceau

**Situation :** `MONT-LE-FRÂNOIS \& VARS · 1743 — 1836`

La souche est paysanne et tient sur deux villages voisins. **Bernard AMYOT**, laboureur, et
**Nicolle BERTAUT** ouvrent le dossier ; leurs parents manquent encore, mais le registre
paroissial de Mont-le-Frânois est accessible pour 1781, et l'on y voit déjà la maison entière :
une sœur aînée, **Françoise AMYOT**, marraine en février 1781 — donc née vers 1768 au plus tard —
et deux frères, Jean-Baptiste et François Bernard, l'un cultivateur, l'autre propriétaire, âgés
de vingt-neuf et vingt-sept ans en 1803.

Le père, **François Bernard AMIOT**, meurt le 5 pluviôse an XI — le 25 janvier 1803 — trois mois
avant le mariage de son fils, ce qui explique qu'il y soit dit décédé. Le mariage **AMIOT ×
RENEVIER**, la même année, est le premier acte que l'on tienne en main et le point d'où tout
descend.

Quatre ans plus tard, l'année 1807 vide l'autre côté de la famille. Le 31 mars, **Catherine
PETITOT** meurt à sept heures du matin ; c'est son mari qui déclare. Le 4 août, **Claude
RENEVIER** meurt à dix-sept heures ; c'est son gendre, **François AMIOT**, vingt-six ans, qui
déclare — et qui nomme au passage les parents du défunt. À trente-deux ans, quatre ans après son
mariage, Barbe est orpheline des deux côtés.

Restent, pour la génération d'avant, deux pistes ouvertes : les PETITOT semblent venir
d'**Écuelle**, à cinq kilomètres de Vars ; et les AMYOT tiennent réciproquement les DENERVAUX sur
les fonts baptismaux à deux mois d'intervalle, en décembre 1780 et février 1781. Deux familles de
laboureurs très proches, et le meilleur fil à tirer.

\---

### II — Fahy-lès-Autrey, tout un siècle

**Situation :** `FAHY-LÈS-AUTREY · 1836 — 1906`

La famille s'installe à Fahy et n'en bouge plus pendant soixante-dix ans. Les cinq recensements
conservés et les tables décennales de 1813 à 1872 donnent à **Claude PAUFARD** et à **Françoise
AMIOT** treize enfants, et non douze : onze meurent avant treize mois, dont deux qu'on croyait
vivants et un treizième entièrement inconnu, mort en 1854. **Une seule fille atteint sûrement
l'âge adulte**, Théolinde. Sa sœur aînée **Clotilde Hortense**, née en 1839, n'apparaît dans
aucune des cinq listes, ni dans aucune table de décès.

Les mêmes sources ouvrent la maison du grand-père : **quatre fils tailleurs de pierre sous un
même toit**, une sœur enfin nommée, une installation à Fahy avancée de douze ans. Elles montrent
surtout Claude PAUFARD **cabaretier** avant d'être propriétaire, puis entrepreneur de travaux
publics — la seule ascension sociale que ce dossier puisse suivre année par année. Son acte de
décès le dit pourtant cafetier jusqu'au bout, et ses parents « défunts », sans les nommer.

Le recensement de 1876 donne la contrepartie du tableau : la grand-mère AMIOT y est
**pensionnaire** là où elle était chef de ménage dix ans plus tôt.

\---

### III — Les GRILLOT sortent du département

**Situation :** `CHAMPVANS-LÈS-DOLE, ANCIER, GRAY · 1743 — 1890`

L'acte de décès de **Thomas GRILLOT**, en 1890, nomme enfin ses parents et le dit **né à Ancier**
et non à Gray — ce qui explique un siècle d'invisibilité dans les tables de la ville. Celui de
son grand-père, en 1825, remonte plus loin encore et le dit né à **Champvans-lès-Dole, dans le
Jura**. **Neuf personnes entrent d'un coup dans l'arbre**, le métier de boucher se suit sur
**cinq générations**, et le prénom Thomas s'explique : il vient d'un cultivateur du Magny,
présent au mariage de sa fille en 1809.

Le mariage de **Marnay**, en 1833, ferme cette génération. Il nomme la mère de Jeanne ÉCARNOT et
date d'un seul coup trois décès — ceux de Noël GRILLOT, de Jean Pierre ÉCARNOT et de Marguerite
GARDOT. Les deux mariés étaient orphelins ; sur six ascendants, **un seul vivait encore** : Anne
Pierre BERNARDOT, bouchère à Gray, qui fait le voyage et signe de sa main.

À Gray, les tables ont livré **quatre maisons GRILLOT distinctes** dont une seule est la nôtre.
Deux homonymes tombent — un résultat négatif, mais qui vaut une trouvaille : il évite qu'une
séance future ne les reprenne.

\---

### IV — L'énigme d'Yvonne

**Situation :** `LYON, SERRIGNY, BEAUNE · 1889 — 1906`

Née fille naturelle à Lyon le 1<sup>er</sup> octobre 1889, elle est reconnue en 1892 par **Victor
Jean-Baptiste CARPENTIER**, voit cette reconnaissance **annulée par le tribunal de Beaune le 14
mai 1897**, puis se fait **adopter par sa propre grand-mère Théolinde**. Trois filiations
successives, juridiquement distinctes, pour une même personne.

Le mariage de 1892 en donne l'explication la plus économique : Carpentier était veuf de
Julie-Lucie GÉNIN, morte le 25 juin 1889, quand Yvonne a été conçue de son vivant. Mais rien
n'établit sa paternité, une tradition familiale l'attribue à un palefrenier du village, et **seul
le jugement de Beaune dira qui a agi et pourquoi**.

Deux questions voisines sont refermées. Celle de la fratrie de Joséphine : elle était fille
unique — MONJEAN, dit « beau-frère de l'épouse » en 1892, avait épousé une CARPENTIER de
Trouvans ; il était beau-frère de l'*époux*, et la mention de l'acte est une erreur de rédaction.
Celle du pharmacien de la tradition orale : c'était Carpentier lui-même, recensé sous le même toit
à Serrigny. La tradition disait vrai, mais avait perdu le nom.

\---

### V — Les VILLETTE, de Paris à l'étude

**Situation :** `PARIS, SELONGEY, FAHY-LÈS-AUTREY · 1840 — 1911`

Les VILLETTE remontent à un **cordonnier né à Paris en 1840** : une entrée parisienne et
artisanale dans un dossier entièrement rural. **Émile Adolphe VILLETTE** meurt à Selongey le 20
mars 1892 ; sa veuve, Joséphine VERNEY, y vit encore quatorze ans plus tard.

Le 22 septembre 1906, à Fahy-lès-Autrey, **Camille Jean VILLETTE** épouse **Yvonne Marguerite
GRILLOT**, seize ans, née à Lyon. Sa mère est présente et consentante ; du côté de l'épouse, la
grand-mère est là aussi — épicière au village, elle avait enterré sa fille l'année précédente.

Le recensement suivant vaut un acte à lui seul. Il donne enfin le métier de Camille Jean :
**huissier**, et « patron » à la colonne du statut — il exerce à son compte. En quatre lignes, la
famille quitte l'artisanat et la terre pour le monde judiciaire, et deux enfants y apparaissent,
nés à Autrey en 1908 et 1911.

\---

### VI — Le XX<sup>e</sup> siècle

**Situation :** `GRAY, DIJON, ANNECY, SAINT-ÉTIENNE · 1930 — 1963`

Deux alliances suffisent à faire sortir la famille de la Haute-Saône. **RIBAUT × VILLETTE**, en
1930, puis **FONTANA × RIBAUT**, le 30 août 1963 à Saint-Étienne : entre les deux, un
département, puis une France entière.

**Simone Camille Henriette RIBAUT**, née le 27 septembre 1933 à Gray, est directrice d'hôpital.
Elle épouse **Marcel Félix FONTANA**, né le 5 octobre 1930 à Annecy, professeur de lettres. Sa
sœur **Françoise**, née à Dijon en 1944, prolonge le mouvement.

Sept générations de laboureurs, de bouchers, de tailleurs de pierre et de cabaretiers tiennent
dans quatre villages ; la huitième naît à Gray, se marie à Saint-Étienne et n'y revient plus. Le
dossier s'arrête ici, non parce que la suite manque, mais parce qu'elle appartient encore aux
vivants.

\---

## 8\. Ce sur quoi il faut me demander

* Si un bloc de contenu existant n'a **pas d'équivalent** dans le prototype et que sa place ne
saute pas aux yeux.
* Si un choix graphique du prototype **contraint le contenu** — une colonne trop étroite pour un
tableau, un composant qui suppose trois éléments là où le site en a douze. Dans ce cas, on
élargit le composant : on ne coupe pas le contenu.
* Si tu dois **supprimer** quoi que ce soit d'autre que l'onglet Frise.

## 9\. Vérifications avant de rendre

* \[ ] Aucun texte généalogique perdu — comparer les compteurs d'actes, de personnes, de pistes
avant et après.
* \[ ] Aucune erreur JavaScript en console, sur chacun des onglets.
* \[ ] L'arbre se déplace, se zoome, s'imprime, et ouvre le tiroir au clic comme avant.
* \[ ] Navigation complète au clavier : onglets aux flèches, tiroir fermable à Échap, focus rendu
au déclencheur.
* \[ ] L'aperçu avant impression sort les panneaux à la suite, sans fond sombre.
* \[ ] Le site reste **un seul fichier `index.html`**, si c'est bien la contrainte actuelle du
dépôt GitHub Pages.

