# ARBRE GÉNÉALOGIQUE — BRANCHE MATERNELLE
# MODIF 29/08 — Fahy et Gray

*Les actes PAUFARD de 1840, 1842 et 1865 · Le recensement de Fahy de 1876 · La remontée de la branche GRILLOT jusqu'au Jura*

---

## 0. Contexte — ce que fait ce patch, en clair

Claude, deux campagnes ont été menées en parallèle depuis le dernier patch. Il faut que tu comprennes ce qu'elles changent avant de toucher au fichier, parce que la seconde modifie la **forme** de l'arbre et pas seulement son contenu.

**Première campagne, à Fahy-lès-Autrey.** On a ouvert cinq actes qui n'étaient jusqu'ici connus que par les tables décennales. Deux d'entre eux datent au jour près les décès de deux enfants PAUFARD que le dernier patch portait au mois seulement. Un troisième — le décès de Claude PAUFARD en 1865 — apporte trois choses : il le dit **cafetier jusqu'à sa mort** (le cabaret de 1841 n'était donc pas une étape traversée, il tenait le café vingt-quatre ans plus tard), il donne enfin l'âge et le domicile de son frère François, et surtout il dit ses parents **« défunts »**, ce qui confirme par acte la fenêtre de décès 1846-1865 qu'on n'avait déduite que du recensement. Un quatrième identifie formellement la sœur, Françoise PAUFARD femme CHATEAU, morte cinq mois après lui. Le cinquième document est le recensement de 1876, qui montre la grand-mère AMIOT devenue pensionnaire chez son gendre là où elle était chef de ménage dix ans plus tôt.

**Seconde campagne, à Gray.** Elle est plus lourde. La branche GRILLOT plafonnait à Thomas, né « 1810-1811 », sans parents ni origine. Elle remonte maintenant de **trois générations** et **sort de la Haute-Saône** : les GRILLOT viennent du Jura, de Champvans-lès-Dole, et le métier de boucher se suit sur cinq générations documentées. Neuf personnes entrent dans l'arbre. Le prénom Thomas s'explique par le grand-père maternel. Et le dépouillement des tables de Gray a fait apparaître **quatre maisons GRILLOT distinctes** dans la même ville, dont une seule est la nôtre — d'où plusieurs pièges d'homonymie qu'il faut inscrire explicitement dans le dossier pour qu'on n'y retombe pas.

**Une règle de méthode à garder en tête pour les gloses.** À Fahy, les tables décennales donnent la date de l'acte, l'événement étant du jour même ou de la veille. **À Gray, ce n'est pas régulier** : certaines lignes portent la date de naissance, d'autres celle de l'acte. On ne peut donc rien dater à Gray sans ouvrir la pièce, et il faut le dire dans l'article des tables.

**Ordre d'exécution suggéré :** §2 et §3 d'abord (les personnes et leurs liens, c'est ce qui change la scène), puis §4 et §5 (les fiches et encarts), puis §6 et §7 (actes et transcriptions), enfin §8 et §9.

---

## 1. Les neuf personnes nouvelles — et pourquoi elles tiennent dans les bandes existantes

Bonne nouvelle avant de commencer : **aucune bande de génération n'est à créer**. Le champ `gen` d'une personne est l'index dans `GENERATIONS`, et les neuf nouvelles se rangent dans des bandes qui existent déjà :

| Personne | `gen` | Bande | Année |
|---|---|---|---|
| Claude GRILLOT, Françoise CHARTON | 0 | −2 (≈ 1710 · 1720) | avant 1745 |
| Pierre Gabriel GRILLOT, Marie Josèphe RÉMY, Thomas BERNARDOT, [Pierrette] ROUGET | 1 | −1 (≈ 1731 · 1743) | ≈ 1745 |
| Noël GRILLOT, Anne Pierre BERNARDOT, Jean Pierre ÉCARNOT | 2 | 0 (1774 · ≈ 1789) | 1779-1789 |

Le libellé de la bande −1 (`yrs:"≈ 1731 · 1743"`) devient un peu étroit avec Pierre Gabriel né vers 1745. **Passe-le à `"≈ 1731 · 1745"`.** Les autres bandes sont bonnes.

### Coordonnées

La grille actuelle est occupée jusqu'à x ≈ 1290 en `gen2`, x ≈ 1160 en `gen1`, x ≈ 1100 en `gen0`. Tout le flanc droit est libre, et c'est là que la branche GRILLOT descend déjà (Thomas est en x = 1430). Les coordonnées ci-dessous sont **une proposition** : si la scène déborde en largeur, ajuste et élargis le canevas, c'est toi qui vois le rendu.

```js
/* ---- gen 0, y = 20 (bande −2) ---- */
{id:"claude-grillot", prenoms:"Claude", nom:"GRILLOT", gen:0, x:1560, y:20, w:210, h:170, neuf:true,
 naissance:{date:"avant 1745", approx:true},
 deces:{date:"avant 1825", note:"dit défunt en mars 1825"},
 notes:[
   {b:"Connu par une seule ligne : l'acte de décès de son fils Pierre Gabriel, en 1825, le dit "
     +"<b>feu Claude Grillot</b>. Ni date, ni lieu, ni métier. C'est le plus ancien GRILLOT du "
     +"dossier.", ferme:true}
 ],
 dossier:[{type:"x", libelle:"Acte non retrouvé"}]},

{id:"francoise-charton", prenoms:"Françoise", nom:"CHARTON", f:true, gen:0, x:1810, y:20, w:210, h:170, neuf:true,
 naissance:{date:"avant 1745", approx:true},
 deces:{date:"avant 1825", note:"dite défunte en mars 1825"},
 notes:[
   {b:"Même source unique que son mari — la filiation portée à l'acte de décès de leur fils en "
     +"1825. Si Pierre Gabriel est né à Champvans-lès-Dole, c'est dans le Jura qu'il faut "
     +"chercher ce couple.", ferme:true}
 ],
 dossier:[{type:"x", libelle:"Acte non retrouvé"}]},

/* ---- gen 1, y = 300 (bande −1) ---- */
{id:"pierre-gabriel-grillot-1745", prenoms:"Pierre Gabriel", nom:"GRILLOT", gen:1, x:1500, y:300, w:230, h:200,
 neuf:true, apports:["Nouveau"],
 naissance:{date:"≈ 1745", lieu:"Champvans-lès-Dole (Jura)", approx:true, note:"80 ans en 1825"},
 deces:{date:"13/03/1825", heure:"6 h", lieu:"Gray", age:"80 ans", note:"en son domicile, sur la place"},
 metiers:[{quoi:"marchand boucher, Gray"}, {quoi:"ancien marchand boucher", an:1825}],
 notes:[
   {b:"<b>C'est lui qui fait sortir la famille du Jura.</b> Son acte de décès est le seul de "
     +"toute la branche à porter un lieu de naissance hors de la Haute-Saône. Les GRILLOT de "
     +"Gray sont donc des arrivants, et la question des origines se déplace d'un département.",
    ferme:true},
   {b:"Il est encore dit <b>époux</b> et non veuf en mars 1825 : Marie Josèphe RÉMY lui survit.",
    ferme:true}
 ],
 dossier:[{type:"n", libelle:"Naissance"}, {type:"d", libelle:"Décès"}]},

{id:"marie-josephe-remy", prenoms:"Marie Josèphe", nom:"RÉMY", f:true, gen:1, x:1760, y:300, w:230, h:200, neuf:true,
 naissance:{date:"dates à établir", approx:true},
 deces:{date:"après mars 1825"},
 notes:[
   {b:"Nommée deux fois : à la publication de mariage de son fils Noël en 1809 et à l'acte de "
     +"décès de son mari en 1825, où elle est dite <b>épouse</b> — elle est donc vivante à "
     +"quatre-vingts ans passés pour lui.", ferme:true}
 ],
 dossier:[{type:"x", libelle:"Acte non retrouvé"}]},

{id:"thomas-bernardot", prenoms:"Thomas", nom:"BERNARDOT", gen:1, x:2020, y:300, w:230, h:200,
 neuf:true, apports:["Nouveau"],
 naissance:{date:"dates à établir", approx:true},
 deces:{date:"après mai 1809"},
 metiers:[{quoi:"cultivateur, Magny"}],
 notes:[
   {b:"<b>C'est de lui que Thomas GRILLOT tient son prénom.</b> Grand-père maternel, "
     +"cultivateur au Magny, il est <i>présent</i> à la publication de mariage de sa fille "
     +"mineure en mai 1809 — la mention est portée à l'acte. Quinze mois plus tard, le premier "
     +"petit-fils porte son nom.", ferme:true}
 ],
 dossier:[{type:"x", libelle:"Acte non retrouvé"}]},

{id:"pierrette-rouget", prenoms:"[Pierrette]", nom:"ROUGET", f:true, gen:1, x:2280, y:300, w:230, h:200,
 neuf:true, doute:true,
 naissance:{date:"dates à établir", approx:true},
 divers:[{dt:"Lecture", dd:"le prénom est <b>incertain sur la publication de 1809</b> — « Pierrette » "
   +"est la lecture la plus probable, à confirmer sur l'acte de mariage"}],
 dossier:[{type:"x", libelle:"Acte non retrouvé"}]},

/* ---- gen 2, y = 569 (bande 0) ---- */
{id:"jean-pierre-ecarnot-1779", prenoms:"Jean Pierre", nom:"ÉCARNOT", gen:2, x:1340, y:569, w:230, h:250,
 neuf:true, apports:["Nouveau"],
 naissance:{date:"≈ 1779", approx:true, note:"environ 32 ans en 1811"},
 metiers:[{quoi:"boucher, Marnay"}],
 notes:[
   {b:"<b>Boucher à Marnay</b>, il déclare lui-même la naissance de sa fille Jeanne en 1811 et "
     +"signe l'acte. Son existence explique le mariage : le boucher de Gray n'épouse pas une "
     +"voisine, il épouse la fille d'un confrère à vingt-cinq kilomètres. <b>C'est une alliance "
     +"de métier.</b>", ferme:true},
   {b:"Son épouse est nommée à l'acte de 1811, mais la vue est trop pâle pour la lire. "
     +"<b>Le nom de la mère de Jeanne reste à relever.</b>", ferme:false}
 ],
 dossier:[{type:"x", libelle:"Acte non retrouvé"}]},

{id:"noel-grillot-1783", prenoms:"Noël", nom:"GRILLOT", gen:2, x:1620, y:569, w:230, h:250,
 neuf:true, apports:["Nouveau"],
 naissance:{date:"29/08/1783", lieu:"Marnay"},
 deces:{date:"1810-1890", note:"dit décédé en février 1890"},
 metiers:[{quoi:"marchand boucher, Gray", an:1809}, {quoi:"boucher, Ancier", an:1810}],
 divers:[
   {dt:"Mariage", dd:"publié à Gray le 7 mai 1809 ; l'acte lui-même reste à retrouver"},
   {dt:"Homonyme", dd:"<b>à ne pas confondre</b> avec le Noël GRILLOT né à Gray en vendémiaire "
     +"an IX, fils de Jacques et de Claudine VALLON, <b>mort à dix-huit jours</b>"}
 ],
 notes:[
   {b:"<b>Le seul candidat possible pour la Grande Armée.</b> Né en août 1783, il relève de la "
     +"classe 1803, en plein cœur des levées de l'Empire. Son père était trop vieux, son fils "
     +"avait quatre ans à Waterloo : si quelqu'un a servi dans cette lignée, c'est lui. Entre "
     +"1803 et 1809 on ne sait rien de sa vie — les registres de recrutement de la Haute-Saône "
     +"trancheront.", ferme:false},
   {b:"Né à Marnay, il y ramène son fils chercher femme : Thomas épousera <b>Jeanne ÉCARNOT, "
     +"née à Marnay</b>. Le lien avec la commune d'origine tient une génération de plus.",
    ferme:true}
 ],
 dossier:[{type:"n", libelle:"Naissance"}, {type:"m", libelle:"Mariage"}, {type:"d", libelle:"Décès"}]},

{id:"anne-pierre-bernardot-1789", prenoms:"Anne Pierre", nom:"BERNARDOT", f:true, gen:2, x:1880, y:569,
 w:230, h:250, neuf:true, apports:["Nouveau"],
 naissance:{date:"≈ 11/03/1789", lieu:"Le Magny", approx:true, note:"jour de lecture incertaine"},
 deces:{date:"avant 1890", note:"dite décédée en février 1890"},
 divers:[
   {dt:"Âges", dd:"20 ans en mai 1809, 22 ans en septembre 1810 — <b>l'écart d'un an est "
     +"ordinaire</b> entre une publication et un acte de naissance"},
   {dt:"Mariage", dd:"<b>mineure</b> en 1809 ; son père était présent et consentant"}
 ],
 dossier:[{type:"n", libelle:"Naissance"}, {type:"d", libelle:"Décès"}]}
```

---

## 2. UNIONS et FILIATIONS

Trois unions nouvelles, toutes établies par acte :

```js
{id:"u-grillot-charton", epoux:["claude-grillot", "francoise-charton"],
 enfants:["pierre-gabriel-grillot-1745"], mariage:null, statut:"établie"},

{id:"u-grillot-remy", epoux:["pierre-gabriel-grillot-1745", "marie-josephe-remy"],
 enfants:["noel-grillot-1783"], mariage:null, statut:"établie"},

{id:"u-bernardot-rouget", epoux:["thomas-bernardot", "pierrette-rouget"],
 enfants:["anne-pierre-bernardot-1789"], mariage:null, statut:"établie"},

{id:"u-grillot-bernardot-1809", epoux:["noel-grillot-1783", "anne-pierre-bernardot-1789"],
 enfants:["thomas-grillot-1810"], mariage:"1809", an:1809,
 acte:"publication du 7 mai 1809", statut:"établie", pw:110}
```

Note que `u-grillot-charton` et `u-grillot-remy` sont dites **établies** et non probables : les deux couples sont nommés comme parents dans un acte d'état civil, ce n'est pas une déduction.

**Le cas ÉCARNOT demande ton jugement.** Jean Pierre ÉCARNOT est le père de Jeanne, mais la mère est illisible sur l'acte de Marnay. Je ne veux pas inventer une épouse, et je ne sais pas si le moteur tolère une union à un seul époux. **Choisis le mécanisme qui marche** — union à `epoux` d'un élément, entrée dans `FILIATIONS`, ou simple mention dans la fiche de Jeanne si les deux premiers cassent le tracé. L'important est que la carte de Jean Pierre existe et que le lien avec Jeanne soit visible. Si tu passes par `FILIATIONS` :

```js
{enfant:"jeanne-escarnot-1810", parent:"jean-pierre-ecarnot-1779",
 statut:"légitime",
 quoi:"Fille de Jean Pierre ÉCARNOT, boucher à Marnay",
 b:"La mère est nommée à l'acte de naissance de 1811, mais la vue est illisible à cet "
   +"endroit. Le lien paternel, lui, est certain : le père déclare et signe."}
```

---

## 3. Fiches existantes à corriger

### 3.1 — `thomas-grillot-1810`

C'est la fiche la plus transformée du patch : elle passe d'un homme approximatif à un homme daté de bout en bout.

```js
 naissance:{date:"03/09/1810", heure:"8 h", lieu:"Ancier"},
 deces:{date:"11/02/1890", heure:"10 h", lieu:"Gray", age:"80 ans",
        note:"en son domicile, rue des Verreries n° 1", neuf:"Daté"},
 metiers:[{quoi:"marchand boucher, Gray"}, {quoi:"propriétaire", an:1890}],
 divers:[
   {dt:"Parents", dd:"<b>Noël GRILLOT</b>, boucher, et <b>Anne Pierre BERNARDOT</b> "
     +"— établi par son acte de décès<span class=\"tag-new\">Nouveau</span>"},
   {dt:"Mariage", dd:"avant décembre 1835"}
 ],
 notes:[
   {b:"<b>Son prénom vient de son grand-père maternel</b>, Thomas BERNARDOT, cultivateur au "
     +"Magny, qui était présent au mariage de sa fille quinze mois avant cette naissance. "
     +"C'est la même mécanique que le Bazille des PAUFARD.<span class=\"tag-new\">Nouveau</span>",
    ferme:true},
   {b:"Absent au mariage de son fils en 1866 : consentement par acte notarié devant "
     +"M<sup>e</sup> [Tonin], à Autrey.", ferme:true},
   {b:"<b>Son décès est déclaré par son fils Joseph, « capitaine en retraite ».</b> C'est "
     +"l'engagé volontaire de 1854, le blessé de Grosmagny, le chevalier de la Légion d'honneur "
     +"de 1872 — revenu à Gray finir sa vie près de son père. Le second déclarant est un juge "
     +"aux tribunaux militaires.<span class=\"tag-new\">Nouveau</span>", ferme:true}
 ],
```

Retire `apports:["Daté"]` s'il fait doublon avec les nouvelles marques.

### 3.2 — `jeanne-escarnot-1810`

Renomme l'identifiant si tu peux le faire proprement — elle est née en 1811, pas 1810 — **mais seulement si tu répercutes la référence dans `u-escarnot-grillot`**. Si c'est risqué, garde l'id et corrige seulement les données. Le `dossier` passe de « acte non retrouvé » à une naissance retrouvée.

```js
 naissance:{date:"1811", lieu:"Marnay", note:"acte n° 24 de 1811", neuf:"Retrouvée"},
 deces:{date:"05/08/1888", heure:"10 h", lieu:"Gray", age:"77 ans",
        note:"en son domicile, rue [Régny ?]", neuf:"Datée"},
 metiers:[{quoi:"sans profession, à Gray"}],
 divers:[
   {dt:"Père", dd:"<b>Jean Pierre ÉCARNOT</b>, boucher à Marnay<span class=\"tag-new\">Nouveau</span>"},
   {dt:"Variante", dd:"<b>ÉCARNOT</b> sur ses propres actes de 1811 et 1888 ; ESCARNOT sur "
     +"l'extrait de 1835 seulement"}
 ],
 notes:[
   {b:"<b>Fille de boucher épousée par un boucher.</b> Née à Marnay, à vingt-cinq kilomètres "
     +"de Gray, elle n'était pas une voisine — mais son beau-père Noël était né à Marnay lui "
     +"aussi. Le mariage suit le métier et la commune d'origine, pas la proximité."
     +"<span class=\"tag-new\">Nouveau</span>", ferme:true},
   {b:"Son décès est déclaré par son fils <b>Joseph Émile</b>, trente-quatre ans, le cadet de "
     +"la fratrie. Thomas lui survivra dix-huit mois.", ferme:true}
 ],
 dossier:[{type:"n", libelle:"Naissance"}, {type:"d", libelle:"Décès"}]
```

### 3.3 — `claude-alexis-paufard-1813`

Une seule correction, mais elle change la lecture du personnage. Le dernier patch présentait le cabaret comme une étape entre la pierre et la propriété. **L'acte de décès de 1865 le dit « propriétaire et cafetier ».** Le café court donc jusqu'au bout.

```js
 metiers:[{quoi:"tailleur de pierre", an:1836},
          {quoi:"<b>cabaretier</b>", an:1841},
          {quoi:"propriétaire", an:1842, note:"et aux recensements de 1846, 1856, 1861"},
          {quoi:"entrepreneur de travaux publics", an:1850, note:"« entrepreneur » en 1854"},
          {quoi:"propriétaire et <b>cafetier</b>", an:1865, neuf:"Corrigé"}],
```

Et remplace la note « Le seul des frères à sortir de l'atelier » par celle-ci, qui dit mieux les choses :

```js
   {b:"<b>Le seul des frères à sortir de l'atelier — et il n'a jamais lâché le café.</b> Ses "
     +"quatre frères taillent encore la pierre sous le toit paternel en 1841 quand il tient un "
     +"cabaret ; il se dit ensuite propriétaire, puis entrepreneur de travaux publics — mais "
     +"son acte de décès, vingt-quatre ans plus tard, le dit encore <i>cafetier</i>. Le débit "
     +"de boissons est le socle, le reste est venu par-dessus.<span class=\"tag-new\">Corrigé</span>",
    ferme:true},
```

Ajoute enfin :

```js
   {b:"Son décès est déclaré par son <b>frère François</b>, quarante-six ans, tailleur de "
     +"pierre domicilié à Autrey, et par <b>Joseph REDOUTET</b>, quarante-trois ans, "
     +"cultivateur, voisin. L'acte confirme sa naissance à <b>Oyrières le 7 juin 1813</b> et "
     +"donne à sa veuve cinquante-quatre ans.<span class=\"tag-new\">Nouveau</span>", ferme:true}
```

### 3.4 — `jean-baptiste-paufard-1788` et `denise-redoutet-1789`

La fenêtre 1846-1865 n'était déduite que du recensement. Elle est maintenant **confirmée par acte** : celui de leur fils, en mai 1865, les dit « défunts […] domiciliés à Fahy-lès-Autrey ». Sur les deux fiches :

```js
 deces:{date:"1846-1865", lieu:"Fahy-lès-Autrey", neuf:"Confirmé"},
```

Et ajoute cette note sur la fiche de Jean-Baptiste, parce que c'est un problème ouvert qu'il ne faut pas laisser filer :

```js
   {b:"<b>On ne trouve leurs décès nulle part.</b> Vivants au recensement de 1846, dits "
     +"défunts et domiciliés à Fahy en mai 1865, ils sont pourtant absents des tables "
     +"décennales de décès de la commune. Trois explications restent ouvertes : Denise y est "
     +"portée à REDOUTET et a pu échapper au dépouillement ; ils ont pu mourir chez leur fils "
     +"à Autrey ; ou à l'hospice de Gray, ce qui n'aurait pas changé leur domicile légal."
     +"<span class=\"tag-new\">Ouvert</span>", ferme:false}
```

### 3.5 — `napoleon-grillot-1838`

Le recensement de 1876 avance d'un cran l'attestation du métier et ajoute un fait de statut :

```js
 metiers:[{quoi:"boucher à Gray", an:1866},
          {quoi:"propriétaire à Fahy", an:1869},
          {quoi:"marchand de bestiaux", an:1876, note:"encore en 1878", neuf:"Corrigé"}],
```

```js
   {b:"<b>Un domestique au foyer en 1876</b> — Joseph TISSOT, trente-cinq ans, né à "
     +"Beaumotte. C'est le premier domestique de tout le dossier : ni le cabaretier ni "
     +"l'entrepreneur n'en avaient eu.<span class=\"tag-new\">Recensement</span>", ferme:true}
```

### 3.6 — `francoise-amiot-1810`

Ajoute au métier et aux notes :

```js
 metiers:[{quoi:"propriétaire"},
          {quoi:"propriétaire, <b>chef de ménage</b>", an:1866},
          {quoi:"<b>chez son gendre</b>", an:1876, note:"« mère de la dame Grillot »", neuf:"Recensement"}],
```

```js
   {b:"<b>Elle finit hébergée là où elle avait régné.</b> Chef de ménage et propriétaire en "
     +"1866, elle n'est plus en 1876 que la quatrième ligne d'un foyer dirigé par son gendre, "
     +"sous la qualification de « mère de la dame Grillot ». Elle meurt deux ans plus tard. "
     +"Entre les deux listes, la maison a changé de mains — c'est le moment exact où les "
     +"PAUFARD cèdent le pas aux GRILLOT.<span class=\"tag-new\">Recensement</span>", ferme:true}
```

### 3.7 — `theolinde-paufard-1843`

Sa ligne « Variantes » disait qu'elle est recensée tantôt PAUFARD tantôt GRILLOT. C'est vérifié sur pièce en 1876, où elle est inscrite **PAUFARD femme Grillot**. Ajoute simplement `<span class="tag-new">Vérifié</span>` à cette ligne. Cette variante n'est pas décorative : elle explique peut-être pourquoi la famille est introuvable au recensement de 1872 (voir §7).

---

## 4. Encarts

### 4.1 — L'encart de la fratrie PAUFARD : deux dates à préciser

Le dernier patch portait deux décès au mois seulement, avec une note disant que les actes restaient à ouvrir. Ils sont ouverts. Dans `encart-fratrie-paufard-treize-enfants` :

```js
   {who:"<b>Marie-Louise</b> Léocadie Nivida",
    yr:"29/01/1840, 15 h · <span class=\"died\">† 27/09/1840</span>"},
   {who:"<b>Claude Alexis</b>",
    yr:"10/07/1842, 16 h · <span class=\"died\">† 26/07/1842</span>"},
```

Et la `note` de l'encart perd sa dernière phrase. Nouvelle version :

```js
 note:"Onze des treize meurent avant treize mois. Après Théolinde, <b>sept naissances de "
     +"suite, sept enfants morts avant trois mois et demi</b>. Le quatrième prénom de "
     +"Marie-Louise, « Nivida », est confirmé par ses deux actes.", noteFerme:true
```

### 4.2 — L'encart des collatéraux : trois lignes à compléter

- **Françoise PAUFARD femme CHATEAU** — la ligne existante gagne sa fin : morte le **7 octobre 1865 à cinquante-trois ans**, cinq mois après son frère. Son mari **Joseph CHATEAU**, cinquante-neuf ans, propriétaire cultivateur, déclare le décès.
- **Nouvelle ligne, « Gendre »** — **Auguste CHATEAU**, vingt-sept ans, cultivateur à Fahy, dit *gendre de la décédée* en 1865. Un CHATEAU a donc épousé une fille CHATEAU : mariage entre cousins, à chercher entre 1858 et 1865.
- **Oncle François PAUFARD** — complète : **quarante-six ans en mai 1865, tailleur de pierre, domicilié à Autrey**, déclarant au décès de son frère. Né vers 1818-1819.
- **Joseph REDOUTET** — complète : **quarante-trois ans en 1865, cultivateur à Fahy**, voisin déclarant. Né vers 1822.

### 4.3 — Nouvel encart : « Les GRILLOT de Gray — quatre maisons »

À placer dans « Le dossier », en `aside--firm`. C'est l'encart le plus utile du patch : il évite qu'on refasse trois fois le même faux rapprochement.

> **Les GRILLOT de Gray — quatre maisons** · *Nouveau*
>
> Le nom est fréquent à Gray, et les tables décennales portent une trentaine de GRILLOT entre 1792 et 1892. **La preuve qu'il y a plusieurs familles est arithmétique** : en décembre 1835, deux naissances GRILLOT sont séparées de six jours ; en 1826, deux autres de quatre mois. Aucune mère ne peut faire cela.
>
> **La nôtre — Pierre Gabriel GRILLOT × Marie Josèphe RÉMY**, marchands bouchers, *sur la place*. Venus de Champvans-lès-Dole, dans le Jura.
>
> **Jacques GRILLOT, boucher × Claudine VALLON** — rue de la Propagande, puis rue des Marseillais, puis rue de Thionville. Enfants relevés : François (1793), Vallier (né à Arc, mort à cinq ans et demi en l'an IX), Noël (mort à dix-huit jours en l'an IX).
>
> **Marie Ferréol GRILLOT × Jeanne Baptiste PREVOT** — place Jemmapes, puis rue Tricolore. Lui est *propriétaire* en 1798, *secrétaire de la mairie* en 1801. Enfants relevés : Anne Marie (1798), Jean Baptiste (1799), Anne Joseph Constantin (1801).
>
> **Joseph GRILLOT × Anne MARCHAND** — connus par le seul registre matricule de leur fils Nicolas, né à Gray en 1777.
>
> **Deux pièges à écarter définitivement.** Le **Noël GRILLOT né à Gray en vendémiaire an IX** n'est pas le nôtre : il est mort à dix-huit jours, fils de Jacques. Et la **Jeanne Pauline GUILLOT** morte à l'hospice de Gray en nivôse an X n'est pas une GRILLOT du tout — enfant de trois mois née à Vesoul, fille de Jeanne Claude Guillot d'Authume et de père inconnu.
>
> **Il n'y a peut-être qu'une seule souche.** Un boucher du Jura ne s'installe pas seul dans une ville. Jacques est boucher comme Pierre Gabriel, Joseph a un fils né à Gray dès 1777. Les actes de décès de Jacques et de Joseph nommeront leurs parents : si l'un des deux est dit fils de Claude GRILLOT et Françoise CHARTON, les quatre maisons n'en font qu'une.

### 4.4 — Nouvel encart : « La lignée des bouchers »

Court, mais c'est l'idée qui structure toute la branche. En `aside--firm` :

> **La lignée des bouchers** · *Nouveau*
>
> **Pierre Gabriel** marchand boucher (≈ 1745-1825) → **Noël** boucher à Ancier, marchand boucher à Gray (1783) → **Thomas** marchand boucher à Gray (1810-1890) → **Napoléon** boucher puis marchand de bestiaux, **Nicolas Eugène** marchand boucher, **Joseph Émile** marchand boucher rue du Marché.
>
> Cinq générations sur un même métier, et l'alliance suit : Thomas épouse la fille de **Jean Pierre ÉCARNOT, boucher à Marnay**. C'est ce qui explique la suite — si Napoléon peut s'établir à Fahy comme *marchand de bestiaux* en 1876, c'est qu'il vend ce que sa famille abat depuis un siècle.

---

## 5. ACTES — quatorze entrées nouvelles

```js
/* ---- Fahy ---- */
{id:"a-1840-deces-de-marie-louise-paufard", type:"d", titre:"Décès de Marie-Louise PAUFARD",
 date:"28 septembre 1840", an:1840, neuf:true, tr:"t-1840-deces-de-marie-louise-paufard",
 mentions:[{qui:"claude-alexis-paufard-1813"}, {qui:"francoise-amiot-1810"}]},

{id:"a-1842-deces-de-claude-alexis-paufard-fils", type:"d",
 titre:"Décès de Claude Alexis PAUFARD, fils", date:"26 juillet 1842", an:1842, neuf:true,
 tr:"t-1842-deces-de-claude-alexis-paufard-fils",
 mentions:[{qui:"claude-alexis-paufard-1813"}, {qui:"francoise-amiot-1810"}]},

{id:"a-1865-deces-de-claude-paufard", type:"d", titre:"Décès de Claude PAUFARD",
 date:"13 mai 1865", an:1865, neuf:true, tr:"t-1865-deces-de-claude-paufard",
 mentions:[{qui:"claude-alexis-paufard-1813", principal:1}, {qui:"francoise-amiot-1810"},
           {qui:"jean-baptiste-paufard-1788"}, {qui:"denise-redoutet-1789"}]},

{id:"a-1865-deces-de-francoise-paufard-femme-chateau", type:"d",
 titre:"Décès de Françoise PAUFARD, femme CHATEAU", date:"8 octobre 1865", an:1865, neuf:true,
 tr:"t-1865-deces-de-francoise-paufard-femme-chateau", mentions:[]},

{id:"a-1876-le-menage-grillot-au-recensement-de-fahy", type:"p",
 titre:"Le ménage GRILLOT au recensement de Fahy", date:"1876", an:1876, neuf:true,
 tr:"t-1876-le-menage-grillot-au-recensement-de-fahy",
 mentions:[{qui:"napoleon-grillot-1838", principal:1}, {qui:"theolinde-paufard-1843", principal:1},
           {qui:"josephine-grillot-1869"}, {qui:"francoise-amiot-1810", principal:1}]},

/* ---- Gray, Ancier, Marnay ---- */
{id:"a-1793-1802-les-deux-maisons-grillot-de-gray", type:"n",
 titre:"Les deux maisons GRILLOT de Gray", date:"an II — an X", an:1799, neuf:true,
 tr:"t-1793-1802-les-deux-maisons-grillot-de-gray", mentions:[]},

{id:"a-1809-publication-de-mariage-de-noel-grillot", type:"m",
 titre:"Publication de mariage de Noël GRILLOT", date:"7 mai 1809", an:1809, neuf:true,
 tr:"t-1809-publication-de-mariage-de-noel-grillot",
 mentions:[{qui:"noel-grillot-1783", principal:1}, {qui:"anne-pierre-bernardot-1789", principal:1},
           {qui:"pierre-gabriel-grillot-1745"}, {qui:"marie-josephe-remy"},
           {qui:"thomas-bernardot"}, {qui:"pierrette-rouget"}]},

{id:"a-1810-naissance-de-thomas-grillot", type:"n", titre:"Naissance de Thomas GRILLOT",
 date:"3 septembre 1810", an:1810, neuf:true, tr:"t-1810-naissance-de-thomas-grillot",
 mentions:[{qui:"thomas-grillot-1810", principal:1}, {qui:"noel-grillot-1783", principal:1},
           {qui:"anne-pierre-bernardot-1789", principal:1}]},

{id:"a-1811-naissance-de-jeanne-ecarnot", type:"n", titre:"Naissance de Jeanne ÉCARNOT",
 date:"1811", an:1811, neuf:true, tr:"t-1811-naissance-de-jeanne-ecarnot",
 mentions:[{qui:"jeanne-escarnot-1810", principal:1}, {qui:"jean-pierre-ecarnot-1779", principal:1}]},

{id:"a-1825-deces-de-pierre-gabriel-grillot", type:"d",
 titre:"Décès de Pierre Gabriel GRILLOT", date:"13 mars 1825", an:1825, neuf:true,
 tr:"t-1825-deces-de-pierre-gabriel-grillot",
 mentions:[{qui:"pierre-gabriel-grillot-1745", principal:1}, {qui:"marie-josephe-remy"},
           {qui:"claude-grillot", principal:1}, {qui:"francoise-charton", principal:1}]},

{id:"a-1888-deces-de-jeanne-ecarnot", type:"d", titre:"Décès de Jeanne ÉCARNOT",
 date:"6 août 1888", an:1888, neuf:true, tr:"t-1888-deces-de-jeanne-ecarnot",
 mentions:[{qui:"jeanne-escarnot-1810", principal:1}, {qui:"thomas-grillot-1810"}]},

{id:"a-1890-deces-de-thomas-grillot", type:"d", titre:"Décès de Thomas GRILLOT",
 date:"11 février 1890", an:1890, neuf:true, tr:"t-1890-deces-de-thomas-grillot",
 mentions:[{qui:"thomas-grillot-1810", principal:1}, {qui:"jeanne-escarnot-1810"},
           {qui:"noel-grillot-1783", principal:1}, {qui:"anne-pierre-bernardot-1789", principal:1}]},

{id:"a-an9-matricule-de-nicolas-grillot", type:"x",
 titre:"Registre matricule de Nicolas GRILLOT", date:"an IX — an XII", an:1801, neuf:true,
 tr:"t-an9-matricule-de-nicolas-grillot", mentions:[]},

{id:"a-1792-1892-les-grillot-dans-les-tables-decennales-de-gray", type:"d",
 titre:"Les GRILLOT dans les tables décennales de Gray", date:"1792-1892", an:1838, neuf:true,
 tr:"t-1792-1892-les-grillot-dans-les-tables-decennales-de-gray",
 mentions:[{qui:"napoleon-grillot-1838"}, {qui:"thomas-grillot-1810"}]}
```

**Compteur :** l'onglet Transcriptions passe de **71 à 85**.

**Séparateurs :**
- La section **IV** accueille les décès de 1840 et 1842, à leur place chronologique.
- La section **V — Fahy-lès-Autrey, 1865-1906** accueille les deux décès de 1865 en tête, et le recensement de 1876 après.
- La section **VI** est à renommer : `VI — Gray, Ancier et Marnay, 1793-1890 — les GRILLOT`. Les huit nouveaux articles GRILLOT s'y rangent par ordre chronologique, avant les pièces de 1833-1882 qui s'y trouvent déjà. Aucune autre section n'est renumérotée.

---

## 6. Les quatorze transcriptions

Les textes ci-dessous sont prêts à poser. Les passages entre crochets sont des lectures douteuses : **conserve les crochets**, ils font partie de l'information.

### 6.1 · `t-1840-deces-de-marie-louise-paufard`
**Décès de Marie-Louise PAUFARD** — 28 septembre 1840 — *Fahy-lès-Autrey, décès de 1840, acte n° 24* — étiquettes : Acte de décès · Fratrie PAUFARD

> L'an mil huit cent quarante, le vingt-huit du mois de septembre, à deux heures du soir, par devant nous Joseph Gonget, maire de la commune de Fahy-lès-Autrey, canton d'Autrey, arrondissement de Gray, département de la Haute-Saône, ont comparu les sieurs **Claude Paufard, âgé de vingt-six ans, propriétaire**, et **Jean-Baptiste Roy, âgé de vingt-huit ans, instituteur primaire**, le premier père et le second voisin de la décédée ci-après nommée, demeurant tous les deux en cette commune ; lesquels nous ont déclaré que **le jour d'hier, à six heures du matin, Marie-Louise-Léocadie-Nivida Paufard, âgée d'environ huit mois**, fille dudit Paufard, déclarant, et de Françoise Amiot, est décédée au domicile de ses dits père et mère, ainsi que nous nous en sommes assuré ; et ont, lesdits déclarants, signé avec nous le présent acte de décès, après que lecture en a été faite.
> *Signé : Roy — Paufard — Le Maire Gonget*

**Glose :** Elle est morte le 27 septembre à six heures du matin, née le 29 janvier — huit mois tout juste, comme le dit l'acte. Deux choses se règlent ici. La table décennale portait le 28 : elle donnait bien la date de l'acte, et le décès était de la veille, ce qui valide la convention posée au patch précédent. Et le quatrième prénom, lu « Nivida » avec un point d'interrogation sur l'acte de naissance, est ici répété en toutes lettres : **la lecture est bonne, le doute tombe.**

### 6.2 · `t-1842-deces-de-claude-alexis-paufard-fils`
**Décès de Claude Alexis PAUFARD, fils** — 26 juillet 1842 — *Fahy-lès-Autrey, décès de 1842, acte n° 17* — étiquettes : Acte de décès · Fratrie PAUFARD

> L'an mil huit cent quarante-deux, le vingt-six du mois de juillet, à neuf heures du matin, par devant nous Joseph Gonget, maire et officier de l'état civil de la commune du Fahy-lès-Autrey, canton d'Autrey, arrondissement de Gray, département de la Haute-Saône, ont comparu les sieurs **Jean-Baptiste Roy, âgé de trente ans, instituteur communal**, et **Claude Alexis Paufard, âgé de vingt-neuf ans, propriétaire**, demeurant tous deux en cette commune, **le premier voisin et le second père** du décédé ci-après nommé ; lesquels nous ont déclaré que **ce présent jour, à huit heures du matin, Claude Alexis Paufard, âgé de quinze jours**, fils dudit Paufard, déclarant, et de Françoise Amiot, son épouse, est décédé au domicile de ses dits père et mère, ainsi que nous nous en sommes assuré ; et ont, les dits déclarants, signé avec nous le présent acte de décès, après lecture.
> *Signé : Roy — Paufard — Le Maire Gonget*

**Glose :** L'enfant meurt à huit heures du matin, l'acte est dressé à neuf. **Une heure.** C'est le seul acte de la série où le délai est nul, et le seul où le père passe en second — l'instituteur Roy est cité le premier, comme s'il avait fallu quelqu'un pour mener Claude Alexis à la maison commune. Il vient déclarer la mort d'un enfant qui portait ses deux prénoms. Il y reviendra huit fois.

### 6.3 · `t-1865-deces-de-claude-paufard`
**Décès de Claude PAUFARD** — 13 mai 1865 — *Fahy-lès-Autrey, décès de 1865, acte n° 1* — étiquettes : Acte de décès · Filiation · Profession

> *En marge :* N° 1<sup>er</sup> — Décès de **Paufard Claude, marié, âgé de 51 ans, du 12 mai**.
>
> L'an mil huit cent soixante-cinq, le treize mai à huit heures du matin, devant nous **Boisset Jean-François, maire**, officier de l'état civil de la commune de Fahy-lès-Autrey, canton d'Autrey (Haute-Saône), ont comparu en la maison commune **Paufard François, âgé de quarante-six ans, tailleur de pierre, domicilié à Autrey, frère du défunt** ci-après désigné, et **Redoutet Joseph, âgé de quarante-trois ans, cultivateur, domicilié à Fahy-lès-Autrey**, [voisin du même décédé] ; lesquels nous ont déclaré que **Paufard Claude, âgé de cinquante et un ans, propriétaire et cafetier**, domicilié à Fahy-lès-Autrey, **né à Oyrières le sept juin mil huit cent treize**, **fils de défunts Paufard Jean-Baptiste et de Redoutet Denise, en leur vivant époux, propriétaire, domiciliés à Fahy-lès-Autrey**, et époux de **Amiot Françoise, âgée de cinquante-quatre ans, propriétaire**, domiciliée aussi audit Fahy, **est décédé le jour d'hier à cinq heures du soir, en son domicile**. Après nous être assuré du décès, nous avons aussitôt dressé le présent acte, que les comparants ont signé avec nous après lecture.
> *Signé : Paufard — J. Redoutet — Le Maire Boisset*

**Glose :** Trois choses en douze lignes. La première est un métier : **« propriétaire et cafetier »**. On tenait le cabaret de 1841 pour une étape entre la pierre et la propriété ; vingt-quatre ans plus tard, il tient encore le café. C'est le socle, et le reste est venu par-dessus. La deuxième est un mot : **« défunts »**. Ses parents sont morts, et l'acte les dit domiciliés à Fahy — la fenêtre 1846-1865, qu'on n'avait déduite que du recensement, est confirmée par pièce, et le problème se déplace : où sont leurs actes ? La troisième est un homme. **François PAUFARD, quarante-six ans, tailleur de pierre à Autrey**, vient déclarer la mort de son frère. C'est l'oncle connu depuis le mariage de 1836 et jamais daté : né vers 1818-1819, resté au métier du père quand son aîné le quittait.

### 6.4 · `t-1865-deces-de-francoise-paufard-femme-chateau`
**Décès de Françoise PAUFARD, femme CHATEAU** — 8 octobre 1865 — *Fahy-lès-Autrey, décès de 1865, acte n° 6* — étiquettes : Acte de décès · Collatéraux · **Pièce incomplète**

> *En marge :* N° 6 — Décès de **[Pa]ufard Françoise, [ma]riée, âgée de 53 ans, du 7 octobre**.
>
> L'an mil huit cent soixante-cinq, le huit octobre à huit heures du matin, devant nous Boisset Jean-François, maire, officier de l'état civil de la commune de Fahy-lès-Autrey, canton d'Autrey (Haute-Saône), ont comparu en la maison commune **Chateau Joseph, âgé de cinquante-neuf ans, propriétaire cultivateur, époux de la décédée**, et **Chateau Auguste, âgé de vingt-sept ans, cultivateur, gendre de la même décédée** ci-après nommée, les deux domiciliés à Fahy-lès-Autrey ; lesquels nous ont déclaré que **Paufard Françoise, âgée de cinquante[-trois ans]**… *[la vue s'interrompt ici]*

**Glose :** L'identification était une hypothèse ; elle est établie. La « Paufard Françoise » de la table décennale est bien **la sœur de Claude, épouse de Joseph CHATEAU**, morte le 7 octobre 1865 à cinquante-trois ans — cinq mois après son frère. Née vers 1812, elle était l'aînée. La table se lit d'ailleurs *8 octobre* et non 3 : la lecture précédente était fautive. Et le second déclarant pose une question neuve : **Auguste CHATEAU, vingt-sept ans, dit gendre de la décédée**. Un CHATEAU a donc épousé une fille CHATEAU, entre cousins, quelque part entre 1858 et 1865. **La seconde moitié de cet acte manque**, et c'est elle qui nommerait les parents de Françoise et son lieu de naissance — soit la voie la plus courte vers la génération PAUFARD antérieure à Fahy.

### 6.5 · `t-1876-le-menage-grillot-au-recensement-de-fahy`
**Le ménage GRILLOT au recensement de Fahy** — 1876 — *Fahy-lès-Autrey, liste nominative, maison 23, ménage 25* — étiquettes : Recensement · Profession

> **91.** GRILLOT, *André F<sup>ois</sup> Napoléon* — marchand de bestiaux, chef de ménage — 38 ans — français, né à Gray, H<sup>te</sup> Saône
> **92.** PAUFARD femme Grillot, *Théolinde Adélaïde* — sa femme — 33 ans — id., née dans la commune
> **93.** GRILLOT, *Joséphine* — leur fille — 7 ans — id.
> **94.** AMIOT veuve Paufard, *Françoise* — **mère de la dame Grillot** — 66 ans — id., née à Vars, H<sup>te</sup> Saône
> **95.** TISSOT, *Joseph* — **leur domestique** — 35 ans — né à Beaumotte[-lès-Montbozon ?], H<sup>te</sup> Saône

**Glose :** Cinq lignes qui disent un basculement. En 1866, Françoise AMIOT était *propriétaire, chef de ménage*, sa fille sous son toit ; ici elle est quatrième, sous la qualification de **« mère de la dame Grillot »**, dans un foyer que dirige son gendre. Elle mourra deux ans plus tard. Entre les deux listes, la maison a changé de mains. Napoléon y est **marchand de bestiaux dès 1876** et non 1878, et il emploie **un domestique** — le premier de tout le dossier. La colonne des lieux de naissance, qui n'existait pas sur les formulaires antérieurs, confirme d'un coup trois choses tenues jusque-là de sources indirectes : Napoléon né à Gray, Théolinde et Joséphine nées à Fahy, Françoise née à Vars.
> Cette liste **corrige aussi une de nos conclusions** : la recherche « Les GRILLOT dans les recensements de Fahy », menée sur 1866 et 1872, concluait que ces listes ne pouvaient rien contenir. En 1876, elles contiennent la maisonnée entière.

### 6.6 · `t-1793-1802-les-deux-maisons-grillot-de-gray`
**Les deux maisons GRILLOT de Gray** — an II à an X — *Gray, naissances et décès* — étiquettes : Homonymie · Filiation

> **Naissance de François GRILLOT** — 28 frimaire an II. L'an second de la République française une et indivisible, vingt-huit frimaire, à quatre heures du soir, par-devant moi François Joseph Cournot, officier municipal de la commune de Gray, élu le vingt-un vendémiaire dernier, est comparu en la salle publique de la maison commune **Jacques Grillot, boucher, domicilié dans la municipalité de Gray, section de l'Égalité, rue de la Propagande**, lequel, assisté d'André Joseph L'heureux et de Martin Maître, l'un et l'autre sergents de la commune, le premier âgé de cinquante [ans], le second âgé de soixante-quatre ans, m'a déclaré que **Claudine Vallon, son épouse en légitime mariage**, est accouchée ce présent jour à minuit et demi, dans son domicile situé rue de la Propagande, d'un enfant mâle qu'il m'a présenté et auquel il a donné le prénom de **François**. — *Signé : J. Grillot, Martin Maître, L'heureux, Cournot*
>
> **Naissance de Noël GRILLOT** — 9 vendémiaire an IX. Acte de naissance de **Noël Grillot**, né le huit vendémiaire à dix heures du matin, fils de **Jacques Grillot, boucher, demeurant à Gray, rue des Marseillais**, et de **Claudine Vallon**. Premier témoin, André Joseph L'heureux, sergent de la commune, cinquante-six ans ; second témoin, Toussaint Jaumin, garde de police, cinquante-huit ans. — *Signé : J. Grillot, L'heureux, Jaumin — constaté par Martin, maire*
>
> **Double décès GRILLOT** — 14 brumaire an IX. Acte de décès de **Noël Grillot**, décédé le 26 vendémiaire dernier à une heure du matin, **âgé de dix-huit jours**, né à Gray, demeurant rue de Thionville, fils de Jacques Grillot et de Claudine Vallon. — Acte de décès de **Vallier Grillot**, décédé le treize dudit mois à huit heures du matin, **âgé de cinq ans et demi, né à Arc**, demeurant rue des Marseillais, fils des mêmes. Sur la déclaration de Jacques Grillot, boucher, père, et de Claudine Vallon, mère ; **ont signé, sauf ladite Vallon illettrée**.
>
> **Naissance d'Anne Marie GRILLOT** — 16 prairial an VI. Est comparu **Marie Ferréol Grillot, propriétaire, demeurant à Gray, rue Tricolore**, lequel, assisté d'André Joseph L'heureux, sergent de la commune, et de Toussaint Jaumin, garde champêtre, m'a déclaré que **Jeanne Baptiste Prevot, son épouse en légitime mariage, âgée d'environ vingt-trois ans**, est accouchée ce présent jour à minuit d'un enfant femelle auquel il a donné les prénoms d'**Anne Marie**.
>
> **Naissance de Jean Baptiste GRILLOT** — 2 nivôse an VIII. Par-devant Charles Vincent Beaujot, administrateur municipal, est comparu **Marie Ferréol Grillot, propriétaire, demeurant à Gray, place Jemmapes**, assisté de Jean Claude Peyrot et de la citoyenne Jeanne Baptiste Grillot, lequel déclare que **Jeanne Baptiste Prevot, son épouse, âgée de vingt-[trois] ans**, est accouchée **le jour d'hier à six heures et demie du soir** d'un enfant mâle nommé **Jean Baptiste**.
>
> **Naissance d'Anne Joseph Constantin GRILLOT** — 13 vendémiaire an X. Acte de naissance d'**Anne Joseph Constantin Grillot**, né le douze dudit mois à neuf heures du matin, fils légitime de **Marie Ferréol Grillot, secrétaire de la mairie, demeurant à Gray, place Jemmapes**, et de **Jeanne Baptiste Prevot**. Premier témoin, Anne Josephe Perchet, épouse du citoyen François Martin, instituteur ; second témoin, **Joseph Constantin Dambre, receveur des revenus de ladite ville**.
>
> **À écarter — Décès de Jeanne Pauline GUILLOT** — 7 nivôse an X. Acte de décès de **Jeanne Pauline Guillot**, décédée le même jour à une heure, **âgée de trois mois, née à Vesoul**, demeurant **à l'hospice de Gray où elle est décédée**, **fille de Jeanne Claude Guillot d'Authume et d'un père inconnu**. Sur la déclaration de Joseph Constantin Dambre, receveur, et de Marie Drouaillet, infirmière, illettrée.

**Glose :** Ces six pièces règlent la question de l'homonymie sans laisser de résidu. **Deux ménages GRILLOT vivent à Gray sous le Directoire et le Consulat**, et ils n'ont rien à voir. Jacques est boucher, il change trois fois de rue, sa femme est illettrée, il perd deux enfants dans la même quinzaine de brumaire an IX. Marie Ferréol est propriétaire puis secrétaire de la mairie, il habite place Jemmapes, ses témoins sont l'instituteur et le receveur des revenus de la ville. Ni l'un ni l'autre n'est le nôtre — mais **c'est du côté de Jacques qu'il faut chercher**, car le métier est le même et parce qu'un boucher venu du Jura ne s'installe pas seul dans une ville.
> Deux entrées sortent du corpus par la même occasion. Le **Noël GRILLOT né à Gray en l'an IX** ressemblait à s'y méprendre à notre Noël : il est mort à dix-huit jours. Et la **Jeanne Pauline GUILLOT** de l'hospice n'est pas une GRILLOT du tout ; on la retire.
> *Deux détails à garder.* Le petit **Vallier est né à Arc**, ce qui montre que la maison Jacques bougeait avant de se fixer à Gray. Et le déclarant du décès de l'enfant de l'hospice, **Joseph Constantin Dambre**, est le même homme qui sert de témoin chez Marie Ferréol quelques mois plus tôt et dont le fils porte les prénoms : dans une ville de cette taille, les mêmes quinze personnes signent tout.

### 6.7 · `t-1809-publication-de-mariage-de-noel-grillot`
**Publication de mariage de Noël GRILLOT** — 7 mai 1809 — *Gray, publications de bans* — étiquettes : Mariage · Filiation · **Acte de mariage manquant**

> L'an dix-huit cent neuf, le dimanche **sept du mois de mai**, nous **Joseph Denizot, maire** de la ville de Gray et officier de l'état civil, après nous être transporté devant la principale porte d'entrée de l'hôtel de la mairie, à heure de **onze du matin**, nous avons annoncé et publié, pour la **première** fois, qu'il y a promesse de mariage entre M. **Noël Grillot, marchand boucher**, domicilié à **Gray**, département de la Haute-Saône, **âgé de vingt-cinq ans, né à Marnay**, département du [Doubs], **le vingt-neuf août mil sept cent quatre-vingt-trois**, **fils légitime et majeur de M. Pierre Gabriel Grillot, aussi marchand boucher, demeurant à Gray**, et de dame **Marie Josèphe Rémy** ; et D<sup>elle</sup> **Anne Pierre Bernardot**, domiciliée à [Ma]gny, **âgée de vingt ans, née au Magny le [onze] mars mil sept cent quatre-vingt-neuf**, **fille légitime et mineure de M. Thomas Bernardot, cultivateur, demeurant à Magny**, et de dame **[Pierrette] Rouget**, **le père présent**. Laquelle publication, lue à haute et intelligible voix, a été ensuite affichée à la porte de l'hôtel de la mairie ; de quoi nous avons dressé acte.
> *Signé : Denizot*

**Glose :** **C'est la pièce qui ouvre tout.** En un paragraphe, deux générations arrivent : Pierre Gabriel GRILLOT et Marie Josèphe RÉMY d'un côté, Thomas BERNARDOT et [Pierrette] ROUGET de l'autre. Et le prénom du fils à naître s'explique — quinze mois plus tard, le premier enfant s'appellera **Thomas**, comme le grand-père maternel qui est là, présent, à consentir au mariage de sa fille mineure. Les âges déclarés sont approximatifs de part et d'autre : Noël, né le 29 août 1783, a vingt-cinq ans, ce qui est juste ; Anne Pierre en aura vingt-deux à l'acte de naissance de Thomas quinze mois plus tard. C'est l'ordinaire de ces documents. **L'acte de mariage lui-même reste à retrouver** — il donnera les témoins et, s'il existe, l'état de service du marié.

### 6.8 · `t-1810-naissance-de-thomas-grillot`
**Naissance de Thomas GRILLOT** — 3 septembre 1810 — *Ancier, naissances de 1810, acte n° 13* — étiquettes : Acte de naissance · Filiation

> Du troisième jour du mois de septembre de l'an mil huit cent dix, à huit heures du matin. Acte de naissance de **Thomas Grillot**, né le présent jour à huit heures du matin, fils légitime des sieurs **Noël Grillot, boucher, demeurant en la commune d'Ancier, premier arrondissement du département de la Haute-Saône, âgé de vingt-six ans**, et dame **Anne Pierre Bernardot, son épouse, âgée de vingt-deux [ans]**. Le sexe de l'enfant a été reconnu être masculin. Premier témoin, le sieur **François Villotte, aubergiste** en la commune d'Ancier, âgé de quarante-huit ans. Second témoin, le sieur **[Mamet], manouvrier** en la commune d'Ancier, âgé de trente-six ans. Sur la déclaration à moi faite par le sieur **Noël**, père de l'enfant susnommé, lequel a signé avec les deux témoins après lecture. Constaté suivant la loi par moi **[Robichon]**, maire de la commune d'Ancier faisant les fonctions d'officier public de l'état civil.
> *Signé : Grillot — [Huot] — [Robichon]*

**Glose :** Thomas naît **à Ancier et non à Gray**, ce qui explique pourquoi les tables de la ville ne le portaient pas et pourquoi la branche paraissait sans amont. Ancier est à sept kilomètres de Gray : le jeune ménage s'y est installé au sortir du mariage, le père y est simplement *boucher* quand il se disait *marchand boucher* à Gray l'année précédente. La famille remontera. Détail de rédaction qui vaut d'être noté : l'officier écrit « des sieurs Noël Grillot […] et dame Anne Pierre Bernardot » — la formule est bancale, mais elle nomme les deux parents avec leur âge, ce qui est tout ce qu'on demande.

### 6.9 · `t-1811-naissance-de-jeanne-ecarnot`
**Naissance de Jeanne ÉCARNOT** — 1811 — *Marnay, naissances de 1811, acte n° 24* — étiquettes : Acte de naissance · **Vue à reprendre**

> L'an mil huit cent onze, le [treize] […] par-devant nous François [Samuel Girard], adjoint [faisant fonctions] d'officier de l'état civil de la commune de **Marnay**, est comparu le sieur **Jean Pierre Écarnot, âgé de trente-deux ans [environ], boucher, demeurant à Marnay**, lequel nous a présenté un enfant du sexe féminin né [le jour d'hier] […] de lui et de **[…] son épouse**, auquel il a déclaré vouloir donner le prénom de **Jeanne**. Lesdites déclaration et présentation faites en présence des sieurs **[Pierre Joseph Bouchez]**, âgé de [trente-huit] ans, propriétaire, et **Antoine Corle**, âgé de trente-sept ans, marchand, les deux demeurant à Marnay, [témoins qui ont] signé avec nous après qu'il leur a été fait lecture.
> *Signé : Pierre Écarnot — Bouchez — Antoine Corle — [Girard]*

**Glose :** La fiche de Jeanne portait « acte non retrouvé » et aucune origine ; elle a maintenant une commune, une année et un père. **Jean Pierre ÉCARNOT est boucher à Marnay**, et cela donne au mariage de sa fille son vrai sens : Thomas GRILLOT, boucher de Gray, n'épouse pas une voisine mais la fille d'un confrère à vingt-cinq kilomètres — dans la commune même où son propre père était né en 1783. **Alliance de métier doublée d'un lien d'origine.**
> *La vue est trop pâle sur deux points et il ne faut pas les combler par conjecture :* **le nom de la mère** et la date exacte du mois. Un cliché plus contrasté les donnerait.

### 6.10 · `t-1825-deces-de-pierre-gabriel-grillot`
**Décès de Pierre Gabriel GRILLOT** — 13 mars 1825 — *Gray, décès de 1825, acte n° 39* — étiquettes : Acte de décès · Filiation · Origine

> L'an mil huit cent vingt-cinq, le **treize** du mois de **mars** à quatre heures du soir, par-devant nous Maire de la ville de Gray soussigné, officier de l'état civil, sont comparus MM. **Jean François Patenville, avoué**, domicilié à Gray, âgé de cinquante-trois ans, **voisin** du défunt ; et **Pierre François Bedez, concierge de la mairie**, domicilié à Gray, âgé de quarante-quatre ans, aussi **voisin** du défunt ; lesquels nous ont déclaré que **Pierre Gabriel Grillot, époux de Marie Joseph Rémy, ancien marchand boucher, fils de feus Claude Grillot et Françoise Charton, âgé de quatre-vingts ans, domicilié à Gray, né à [Champvans-lès-Dole], département du Jura**, est décédé le treize du mois de mars de la présente année à six heures du matin **en son domicile, sur la place**, et ont les déclarants signé avec nous le présent acte après lecture.
> *Signé : Patenville — Bedez — [Garnier]*

**Glose :** **L'acte qui fait sortir la famille de la Haute-Saône.** Une seule ligne — « né à Champvans-lès-Dole, département du Jura » — et la branche cesse d'être graylaise : les GRILLOT sont des arrivants, et la recherche des origines change de département. Deux noms viennent avec, **Claude GRILLOT et Françoise CHARTON**, déjà défunts en 1825 : c'est le plus ancien couple du dossier, et il faudra le chercher dans le Jura, dans les registres paroissiaux d'avant 1792.
> Trois détails. L'homme meurt **à quatre-vingts ans**, ce qui le fait naître vers 1745. Il est dit **époux** et non veuf : Marie Josèphe RÉMY lui survit. Et personne de sa famille ne déclare — un avoué et le concierge de la mairie, tous deux voisins. Ses fils étaient bouchers à Ancier et ailleurs ; ce sont les voisins de la place qui l'accompagnent.

### 6.11 · `t-1888-deces-de-jeanne-ecarnot`
**Décès de Jeanne ÉCARNOT** — 6 août 1888 — *Gray, décès de 1888, acte n° 95* — étiquettes : Acte de décès · Origine

> L'an mil huit cent quatre-vingt-huit, le **six** du mois d'**août** à **dix** heures du matin, par-devant nous **Léopold Pierre Couché, adjoint délégué** par arrêté du maire pour remplir les fonctions d'officier de l'état civil de la ville de Gray, département de la Haute-Saône, sont comparus en l'hôtel de ville MM. **Joseph Émile Grillot, fils de la défunte**, domicilié à Gray, âgé de **trente-quatre** ans, et **Jules Jean-Baptiste Laroche, agent de ville**, domicilié à Gray, âgé de **trente et un** ans ; lesquels nous ont déclaré que **Jeanne Écarnot, épouse de Thomas Grillot, ancien boucher à Gray, âgée de soixante-dix-sept ans, domiciliée à Gray, née à Marnay, est décédée le cinq du mois d'août** de la présente année à **dix** heures du matin, **en son domicile à Gray, rue [Régny]**. Après nous être assuré du décès, en nous transportant auprès de la personne décédée, nous avons aussitôt dressé le présent acte que les déclarants ont signé avec nous après lecture.
> *Signé : Grillot Émile — Laroche — L. Couché*

**Glose :** Elle est morte le 5 août 1888 à soixante-dix-sept ans, ce qui la fait naître en 1810 ou 1811 et concorde avec l'acte de Marnay. Son mari est dit **« ancien boucher »** : à soixante-dix-huit ans il a passé la main, et c'est **Joseph Émile**, le cadet de la fratrie, trente-quatre ans, marchand boucher rue du Marché, qui vient déclarer. La mention **« née à Marnay »** vaut confirmation croisée de l'acte de 1811.

### 6.12 · `t-1890-deces-de-thomas-grillot`
**Décès de Thomas GRILLOT** — 11 février 1890 — *Gray, décès de 1890, acte n° 27* — étiquettes : Acte de décès · Filiation · Origine

> L'an mil huit cent quatre-vingt-dix, le **onze** du mois de **février** à **onze** heures du **matin**, par-devant nous **Couché Léopold Pierre**, adjoint délégué par arrêté du maire pour remplir les fonctions d'officier de l'état civil de la ville de Gray, département de la Haute-Saône, sont comparus en l'hôtel de ville MM. **Grillot Joseph, capitaine en retraite**, domicilié à Gray, âgé de **cinquante-cinq** ans, **fils du défunt**, et **[Freyler] Jean Paul Gaspard, juge aux tribunaux militaires**, domicilié à Gray, âgé de cinquante-huit ans, **voisin** du défunt ; lesquels nous ont déclaré que **Grillot Thomas, propriétaire, veuf de Écarnot Jeanne, âgé de quatre-vingts ans, domicilié à Gray, né à Ancier, [fils] des mariés Grillot Noël et Bernardot Anne Pierre, décédés, est décédé le onze du mois de février** de la présente année à **dix** heures du matin, en son domicile, **rue des Verreries n° 1**. Après nous être assuré du décès, en nous transportant auprès de la personne décédée, nous avons aussitôt dressé le présent acte que les déclarants ont signé avec nous après lecture.
> *Signé : [J. Grillot] — [Freyler] — L. Couché*

**Glose :** **La pièce maîtresse de cette campagne.** En une phrase, elle donne à Thomas sa date de naissance approchée, son lieu — **Ancier**, où personne n'avait pensé à chercher — et **ses deux parents nommés**, Noël GRILLOT et Anne Pierre BERNARDOT, l'un et l'autre déjà morts. La branche cessait à lui ; elle remonte désormais de trois générations.
> Le tableau des déclarants mérite qu'on s'y arrête. C'est **Joseph, cinquante-cinq ans, « capitaine en retraite »**, qui vient déclarer la mort de son père : l'engagé volontaire de 1854, le blessé et prisonnier de Grosmagny, le chevalier de la Légion d'honneur de 1872, revenu finir sa vie dans la ville de son père. Le second déclarant est **juge aux tribunaux militaires**. Deux hommes d'uniforme au chevet d'un boucher de quatre-vingts ans — c'est la mesure exacte de ce que cette famille a parcouru en une génération.
> Il meurt à dix heures du matin, l'acte est dressé à onze. Comme pour le petit Claude Alexis de 1842, à Fahy, quarante-huit ans plus tôt.

### 6.13 · `t-an9-matricule-de-nicolas-grillot`
**Registre matricule de Nicolas GRILLOT** — an IX à an XII — *Garde [des Consuls / impériale], matricule n° 1001* — étiquettes : Militaire · **Hors branche**

> **5<sup>e</sup> [compagnie]** — **Grillot Nicolas, fils de Joseph et de Anne Marchand** — grade : **grenadier** — né le **1<sup>er</sup> mars 1777 à Gray**, canton de [Gray], département de la Haute-Saône — taille **1 m 85**.
> *Signalement :* cheveux châtain clair, sourcils idem, front couvert, yeux gris-bleu, nez petit, bouche moyenne, menton rond, visage rond.
> *Services antérieurs à l'admission dans la Garde :* **entré au service le 26 thermidor an IX dans le 5<sup>e</sup> régiment de cavalerie. A précédemment servi comme chirurgien de 3<sup>e</sup> classe à l'armée d'Helvétie**, ayant été requis par les inspecteurs généraux le 22 floréal an VIII, nommé de 2<sup>e</sup> classe par les mêmes inspecteurs le 25 prairial an VIII, et réduit de 3<sup>e</sup> classe par le travail du ministre le 5 vendémiaire an IX. Corps dont il sort immédiatement : 5<sup>e</sup> régiment de cavalerie.
> *Détail du service dans la Garde :* entré le **16 floréal an X**.
> *Observations :* **rayé du contrôle comme déserteur le 28 pluviôse an XII. Rentré et renvoyé au 5<sup>e</sup> régiment de cuirassiers ledit jour 28 pluviôse an XII.**

**Glose :** **Ce n'est pas notre branche**, et il faut le dire d'emblée : Nicolas est fils de Joseph GRILLOT et d'Anne MARCHAND, une quatrième maison graylaise. On le garde au dossier pour deux raisons. La première est qu'il faut savoir ce qu'on a écarté, sans quoi on le retrouvera dans six mois en croyant l'avoir trouvé. La seconde est qu'il donne la mesure de ce que devient un homme de Gray sous le Consulat : chirurgien de troisième classe à l'armée d'Helvétie, rétrogradé par un trait de plume du ministre, versé simple grenadier dans la Garde à un mètre quatre-vingt-cinq — puis **rayé comme déserteur et réintégré aux cuirassiers le jour même**. Un homme qui part et revient sous escorte dans la même journée : la fuite a duré le temps qu'on aille le chercher.
> Pour notre ligne, la chronologie ne laisse qu'un candidat. Thomas avait quatre ans à Waterloo, Pierre Gabriel en avait soixante-dix. **Reste Noël, né le 29 août 1783 : la classe 1803.**

### 6.14 · `t-1792-1892-les-grillot-dans-les-tables-decennales-de-gray`
**Les GRILLOT dans les tables décennales de Gray** — 1792-1892 — *Gray, tables décennales, dix décennies* — étiquettes : Table décennale · Homonymie

> **Avertissement de source.** *Contrairement à Fahy, les tables de Gray ne sont pas régulières : certaines lignes portent la date de la naissance, d'autres celle de l'acte — les deux cas sont vérifiés sur des pièces ouvertes. Aucune date tirée de ces tables ne peut être tenue pour ferme sans l'acte.*
>
> **Naissances.** *1792-1801* — François, 28 frimaire an II · Anne Marie, 16 prairial an VI · Jean Baptiste, 2 nivôse an VIII · Noël, 8 vendémiaire an IX · Anne Joseph Constantin, 12 vendémiaire an X. — *1802-1812* — Jean Baptiste Joseph et Charles Alexis Marie, 26 nivôse an XII (**jumeaux**) · Catherine Charlotte, 16 thermidor an XIII · Anne Josephe Judith, 19 août 1807 · [Grillet] François, 12 décembre 1809 · mort-né, 27 octobre 1811. — *1813-1822* — Anne Josephe, 13 septembre 1815 · Claudine Fanette Caroline, 12 juin 1816 · Jeanne, 17 août 1818 · André, [1<sup>er</sup>] décembre 1820. — *1823-1832* — [Grillet] Bénigne, 24 septembre 1822 · Charlotte, 31 mars 1823 · Charles-Joseph-Ernest, 24 février 1826 · Joseph, 26 juin 1826 · Marguerite, 4 juin 1829 · Marguerite, 1<sup>er</sup> avril 1831. — *1833-1842* — Françoise Adélaïde, 20 septembre 1833 · Christine, 10 février 1834 · Anne Baptiste, 10 décembre 1835 · Joseph, 16 décembre 1835 · François, 14 février 1837 · **François André Napoléon, 29 janvier 1838** · Anne Louise, 9 février 1840 · Alfred Nicolas, 17 février 1842.
>
> **Mariages.** *1792-1801* — Grillot [Marie] et Jean Baptiste [Prevot], 11 fructidor an V. — *1823-1832* — Grillot François, marié à Anne-Françoise [Chevenin], 2 juin 1824.
>
> **Décès.** *1792-1801* — François, 29 nivôse an II · Jeanne Pauline [Guillot], 7 nivôse an X. — *1802-1812* — Anne Charlotte [Nicole], 20 avril 1810 · mort-né, 27 octobre 1811 · Gabrielle, 15 juillet 1812. — *1822-1832* — Anne Joseph Constantin, 23 novembre 1823 · Xavier, 22 juin 1824 · Charlotte, 10 septembre 1824 · Pierre Gabriel, 13 mars 1825 · Charles-Joseph-Ernest, 12 août 1826 · Pierre-François, 29 octobre 1827 · Marguerite, 22 mars 1830 · Claudine, 27 août 1830 · Noël, 6 février 1832. — *1833-1842* — Antoine, 6 avril 183[4] · Anne Baptiste, 30 décembre 1835 · mort-né, 11 février 1835 · François, 19 décembre 1835 · François, 27 mars 1837. — *1863-1872* — Nicolas-Louis, 5 avril 1865 · Christine, 17 juillet 1868 · Pierre-Joseph, 8 mars 1870. — *1873-1882* — Anne Marie, 17 février 1874 · Ernest Jean Antoine, 3 janvier 1879 · Joséphine, 13 décembre 1879. — *1883-1892* — [Grillet] François, 4 juin 1883 · Charles Eugène Léon, 16 janvier 1883 · **Écarnot Jeanne, 6 août 1888** · **Thomas, 11 février 1890**.

**Glose :** **La preuve de l'homonymie est arithmétique, et elle tient en deux lignes.** En décembre 1835, deux naissances GRILLOT sont séparées de **six jours** ; en 1826, deux autres de **quatre mois**. Aucune mère ne peut faire cela : il y a donc au moins deux familles, simultanément, à trente ans d'écart. Les actes l'ont confirmé depuis.
> *Un piège dont il faut se garder, parce qu'il ressemble à une preuve et n'en est pas :* Marguerite naît en juin 1829, une Marguerite meurt en mars 1830, une autre naît en avril 1831. Ce n'est pas deux familles, c'est le comportement normal d'une seule qui redonne le prénom après un deuil — exactement comme les PAUFARD l'ont fait avec Clotilde.
> *Trois noms voisins à ne pas verser au corpus :* **GRILLET** (Bénigne 1822, François 1809, François mort en 1883), ainsi que GRIFFONNET et GRISON. Et **GILLOT**, dont le bloc des décès de 1813-1822 avait d'abord été pris pour du GRILLOT : c'est une famille distincte, et **les décès GRILLOT de cette décennie restent entièrement à dépouiller** — c'est précisément la fenêtre où pourraient tomber Jacques GRILLOT et sa femme.
> *Une observation à ne pas surinterpréter :* aucun **Thomas** ne figure dans les naissances de 1802-1812. On sait maintenant pourquoi — il est né à Ancier —, mais cela reste le signe qu'il faut se méfier de ces tables pour établir une absence.

---

## 7. Onglet Recherches

### 7.1 — Résolues

> **Qui sont les parents de Thomas GRILLOT ?** — dossier `grillot-paufard`. **Noël GRILLOT, boucher, et Anne Pierre BERNARDOT**, tous deux décédés avant 1890. Établi par son acte de décès, qui donne aussi son lieu de naissance : **Ancier**, et non Gray, ce qui explique un siècle d'invisibilité dans les tables de la ville. `piece: a-1890-deces-de-thomas-grillot`

> **D'où viennent les GRILLOT ?** — dossier `grillot-paufard`. **Du Jura.** L'acte de décès de Pierre Gabriel, en 1825, le dit né à Champvans-lès-Dole. La branche cesse d'être haut-saônoise et remonte à un couple **Claude GRILLOT × Françoise CHARTON**, déjà défunt en 1825, à chercher dans les registres paroissiaux jurassiens. `piece: a-1825-deces-de-pierre-gabriel-grillot`

> **Y a-t-il plusieurs familles GRILLOT à Gray ?** — dossier `grillot-paufard`. **Au moins quatre maisons**, dont trois nommées par acte : Jacques × Claudine VALLON (bouchers), Marie Ferréol × Jeanne Baptiste PREVOT (propriétaire puis secrétaire de mairie), Joseph × Anne MARCHAND, et la nôtre. La démonstration est arithmétique avant d'être documentaire : deux naissances à six jours d'intervalle en décembre 1835. `piece: a-1793-1802-les-deux-maisons-grillot-de-gray`

> **D'où vient Jeanne ESCARNOT ?** — dossier `grillot-paufard`. **De Marnay, fille de Jean Pierre ÉCARNOT, boucher.** Sa fiche portait « acte non retrouvé » et aucune origine. Et le mariage prend son sens : le beau-père de Thomas exerce le même métier que son père, dans la commune même où celui-ci était né. `piece: a-1811-naissance-de-jeanne-ecarnot`

> **Quand meurent Thomas GRILLOT et Jeanne ÉCARNOT ?** — dossier `grillot-paufard`. **Jeanne le 5 août 1888 à soixante-dix-sept ans, Thomas le 11 février 1890 à quatre-vingts.** Le dossier les portait à « avant 1900 » par déduction. `piece: a-1890-deces-de-thomas-grillot`

> **Qui est la « Paufard Françoise » morte en octobre 1865 à Fahy ?** — dossier `grillot-paufard`. **La sœur de Claude, épouse de Joseph CHATEAU**, morte le 7 octobre 1865 à cinquante-trois ans, cinq mois après lui. L'hypothèse posée sur la seule table est vérifiée par l'acte. `piece: a-1865-deces-de-francoise-paufard-femme-chateau`

> **Quand exactement meurent Marie-Louise et Claude Alexis fils ?** — dossier `grillot-paufard`. **Le 27 septembre 1840 à six heures du matin, et le 26 juillet 1842 à huit heures du matin.** Les deux actes sont ouverts, les dates ne sont plus au mois. Ils confirment au passage la convention posée pour Fahy : la table donne la date de l'acte, l'événement est du jour même ou de la veille. `piece: a-1842-deces-de-claude-alexis-paufard-fils`

### 7.2 — Négatives (conséquence obligatoire)

> **Thomas GRILLOT n'est pas né à Gray.** Cherché dans les tables de naissances de Gray des décennies 1802-1812. **Conséquence :** il est né à **Ancier**, à sept kilomètres, où son père s'était établi au sortir du mariage. Plus largement, **les GRILLOT de Gray antérieurs à 1810 ne sont pas les nôtres** sauf preuve contraire : ce sont les maisons Jacques, Marie Ferréol et Joseph. Ne pas les rattacher par proximité de nom.

> **Le Noël GRILLOT né à Gray en l'an IX n'est pas le nôtre.** Il portait le bon prénom et la bonne décennie. **Conséquence :** il est **mort à dix-huit jours**, fils de Jacques GRILLOT et de Claudine VALLON. Notre Noël est né à **Marnay le 29 août 1783**. Piste close.

> **Jeanne Pauline GUILLOT n'est pas une GRILLOT.** Relevée à la table des décès de l'an X. **Conséquence :** enfant de trois mois, née à Vesoul, morte à l'hospice de Gray, **fille de Jeanne Claude Guillot d'Authume et de père inconnu**. À retirer du corpus GRILLOT.

> **Le registre matricule n° 1001 n'est pas de notre branche.** **Conséquence :** Nicolas GRILLOT, grenadier, est fils de **Joseph et d'Anne MARCHAND** — la quatrième maison graylaise. Sa carrière militaire, si tentante soit-elle pour l'hypothèse Grande Armée, **ne prouve rien sur notre ligne**. La question reste entière et se joue sur Noël.

> **À réécrire — `grillot-recensements-fahy`.** L'entrée conclut que les recensements de Fahy « ne peuvent rien contenir » sur les GRILLOT ; son champ `ou` précise pourtant qu'elle n'a porté que sur 1866 et 1872. **Le recensement de 1876 contient la maisonnée entière.** La conséquence était trop générale et doit devenir : *le raisonnement vaut pour 1866, où Napoléon est encore boucher à Gray et où le ménage de Fahy est tenu par la veuve AMIOT — vérifié sur pièce. Il ne vaut pas au-delà : la famille est présente en 1876. La série reste donc active pour 1881 et suivants, et l'absence de 1872 devient un problème à part entière.*

### 7.3 — À faire

> **P1 — Noël GRILLOT dans les registres de recrutement, classe 1803.** `grillot-paufard`
> **Où :** AD Haute-Saône, série R, listes de tirage au sort et registres de recrutement des classes de l'Empire, canton de Gray ou de Marnay, au nom de GRILLOT Noël, né à Marnay le 29 août 1783. Au besoin, contrôles de troupes du SHD à Vincennes.
> **Pourquoi :** c'est **le seul test possible** de l'hypothèse qui a lancé toute cette campagne. Le père était trop vieux, le fils avait quatre ans à Waterloo : si quelqu'un de cette lignée a servi sous l'Empire, c'est Noël, et on ne sait rien de sa vie entre 1803 et 1809. Le registre dira s'il a tiré, s'il est parti, ou s'il s'est fait remplacer. **S'il a servi, le petit-fils baptisé Napoléon en 1838 cesse d'être une mode et redevient un hommage.**

> **P1 — Décès de Jacques GRILLOT et de Joseph GRILLOT à Gray.** `grillot-paufard`
> **Où :** tables décennales de décès de Gray, 1813-1822 en priorité — décennie dont le bloc GRILLOT n'a jamais été dépouillé, celui qui l'a été par erreur étant GILLOT — puis 1823-1832.
> **Pourquoi :** ces deux actes nommeront leurs parents. **Si l'un des deux est dit fils de Claude GRILLOT et de Françoise CHARTON, les quatre maisons graylaises n'en font qu'une**, et tout le corpus des tables se réorganise autour d'une seule fratrie venue du Jura. C'est la question structurante de la branche.

> **P2 — Acte de mariage Noël GRILLOT × Anne Pierre BERNARDOT, 1809.** `grillot-paufard`
> **Où :** Gray, mariages de mai-juin 1809 ; à défaut Magny, commune de la mariée.
> **Pourquoi :** on n'a que la publication des bans. L'acte donnera les témoins, les âges exacts et, s'il y a lieu, la mention d'un congé militaire — croisement direct avec la recherche précédente.

> **P2 — Naissance de Pierre Gabriel GRILLOT à Champvans-lès-Dole, vers 1745.** `grillot-paufard`
> **Où :** AD Jura, registres paroissiaux de Champvans-lès-Dole, 1740-1750.
> **Pourquoi :** c'est la porte d'entrée dans le Jura et le seul moyen d'atteindre Claude GRILLOT et Françoise CHARTON. Vérifier d'abord la lecture du nom de la commune sur l'acte de 1825, qui n'est pas certaine.

> **P2 — Décès de Noël GRILLOT et d'Anne Pierre BERNARDOT.** `grillot-paufard`
> **Où :** Ancier et Gray, entre 1810 et 1890 — ils sont dits décédés en février 1890.
> **Pourquoi :** la fenêtre est de quatre-vingts ans, ce qui est inconfortable. Leurs actes donneraient les parents d'Anne Pierre en confirmation, et surtout diraient si le couple est resté à Ancier ou remonté à Gray, ce qui oriente toutes les autres recherches sur cette génération.

> **P2 — La seconde moitié de l'acte de décès de Françoise PAUFARD femme CHATEAU.** `grillot-paufard`
> **Où :** Fahy-lès-Autrey, décès de 1865, acte n° 6, bas de la page.
> **Pourquoi :** c'est là que seront nommés ses parents et **son lieu de naissance**, qui dira où était la famille PAUFARD vers 1812, avant Fahy — probablement Oyrières. Voie la plus courte vers la génération antérieure de cette branche.

> **P2 — Où sont morts Jean-Baptiste PAUFARD et Denise REDOUTET ?** `grillot-paufard`
> **Où :** dans cet ordre — tables de décès de Fahy 1843-1852 et 1853-1862, **à la lettre R pour Denise**, qui y sera portée à REDOUTET et non à PAUFARD ; puis Autrey-lès-Gray, où vit leur fils François ; puis Gray, à cause de l'hospice, où l'on meurt en gardant son domicile légal ailleurs ; puis les tables de successions et absences du bureau de Gray, qui portent une date de décès pour tout défunt laissant des biens.
> **Pourquoi :** l'acte de 1865 les dit défunts **et domiciliés à Fahy**. S'ils ne sont pas dans les tables de la commune, c'est que le dépouillement a manqué quelque chose ou qu'ils sont morts ailleurs en gardant leur domicile — les deux hypothèses se testent. Leurs actes nommeraient leurs propres parents, seule voie connue vers la génération −1 des PAUFARD.

> **P3 — Le ménage GRILLOT au recensement de Fahy de 1872.** `grillot-paufard`
> **Où :** liste nominative de 1872, en cherchant **sous PAUFARD** et sous les variantes GRILLOZ, GRILLIOT, GRILLOD.
> **Pourquoi :** Joséphine naît à Fahy en mars 1869, Napoléon y est propriétaire la même année, la maisonnée y est en 1876 — une absence en 1872 n'a pas de sens. Or la fiche de Théolinde note qu'elle est recensée tantôt PAUFARD tantôt GRILLOT. **Le test qui tranche : Françoise AMIOT veuve PAUFARD doit figurer dans cette liste**, puisqu'elle est à Fahy en 1866 et y meurt en 1878. Si elle n'y est pas non plus, ce n'est pas la famille qui manque, c'est la liste.

> **P3 — Recensement de Fahy de 1881.** `grillot-paufard`
> **Pourquoi :** Françoise AMIOT meurt en 1878. La liste suivante dira ce que devient la maison après elle, et si le domestique reste.

> **P3 — Mariage Auguste CHATEAU × une fille CHATEAU, 1858-1865.** `grillot-paufard`
> **Où :** Fahy et communes voisines.
> **Pourquoi :** l'acte de 1865 dit Auguste CHATEAU, vingt-sept ans, *gendre* de Françoise PAUFARD. Un CHATEAU a épousé une fille CHATEAU. L'acte nommera la fille et éclairera la descendance de la tante.

> **P3 — La mère de Jeanne ÉCARNOT.** `grillot-paufard`
> **Où :** Marnay, naissances de 1811, acte n° 24 — reprendre le cliché avec plus de contraste.
> **Pourquoi :** le nom est porté à l'acte mais la vue est illisible à cet endroit. C'est une génération complète de la branche maternelle ÉCARNOT qui tient dans ces trois mots.

---

## 8. Séance, chapeau, points de vigilance

### 8.1 — Nouvelle séance

```js
{date:"28-29/08/2026", titre:"Seizième séance — Fahy, puis Gray : la remontée GRILLOT",
 actes:[
  {grp:"Fahy-lès-Autrey"},
  {quoi:"<b>Décès 1840, acte n° 24</b> — Marie-Louise Léocadie Nivida PAUFARD"},
  {quoi:"<b>Décès 1842, acte n° 17</b> — Claude Alexis PAUFARD, fils"},
  {quoi:"<b>Décès 1865, acte n° 1</b> — Claude PAUFARD, « propriétaire et cafetier »"},
  {quoi:"<b>Décès 1865, acte n° 6</b> — Françoise PAUFARD, femme CHATEAU (partiel)"},
  {quoi:"<b>Recensement de 1876</b> — ménage 25"},
  {grp:"Gray — tables décennales"},
  {quoi:"<b>Dix décennies dépouillées</b>, naissances, mariages et décès, 1792-1892"},
  {grp:"Gray — actes"},
  {quoi:"<b>Naissances</b> — François an II, Anne Marie an VI, Jean Baptiste an VIII, Noël an IX, Constantin an X"},
  {quoi:"<b>Décès brumaire an IX</b> — Noël et Vallier GRILLOT, enfants de Jacques"},
  {quoi:"<b>Décès nivôse an X</b> — Jeanne Pauline GUILLOT, écartée du corpus"},
  {quoi:"<b>Publication de mariage du 7 mai 1809</b> — Noël GRILLOT × Anne Pierre BERNARDOT"},
  {quoi:"<b>Décès 1825, acte n° 39</b> — Pierre Gabriel GRILLOT, né dans le Jura"},
  {quoi:"<b>Décès 1888, acte n° 95</b> — Jeanne ÉCARNOT"},
  {quoi:"<b>Décès 1890, acte n° 27</b> — Thomas GRILLOT"},
  {grp:"Ancier et Marnay"},
  {quoi:"<b>Naissance 1810, acte n° 13</b> — Thomas GRILLOT, à Ancier"},
  {quoi:"<b>Naissance 1811, acte n° 24</b> — Jeanne ÉCARNOT, à Marnay"},
  {grp:"Militaire"},
  {quoi:"<b>Registre matricule n° 1001</b> — Nicolas GRILLOT, hors branche"}
 ]},
```

### 8.2 — Chapeau

À ajouter :

> La branche GRILLOT ne s'arrête plus à Thomas. Son acte de décès de 1890 nomme ses parents et le dit **né à Ancier** ; celui de son grand-père, en 1825, fait sortir la famille du département : **les GRILLOT viennent de Champvans-lès-Dole, dans le Jura**. Neuf personnes entrent dans l'arbre, le métier de boucher se suit sur **cinq générations**, et le prénom Thomas s'explique enfin — il vient d'un cultivateur du Magny présent au mariage de sa fille en 1809. À Gray, les tables ont livré **quatre maisons GRILLOT distinctes** dont une seule est la nôtre. À Fahy, l'acte de décès de Claude PAUFARD le dit **cafetier jusqu'au bout** et ses parents « défunts », et le recensement de 1876 montre la grand-mère AMIOT devenue pensionnaire là où elle était chef de ménage.

### 8.3 — Points de vigilance

Ces lectures sont douteuses et **doivent rester marquées** dans le fichier — n'aplanis pas les crochets :

- **[Champvans-lès-Dole]** — la commune jurassienne à l'acte de 1825. C'est le pivot de toute la remontée ; si la lecture est fausse, la piste jurassienne l'est aussi.
- **[Pierrette] ROUGET** — prénom de l'aïeule maternelle, publication de 1809.
- **le [onze] mars 1789** — jour de naissance d'Anne Pierre BERNARDOT.
- **la mère de Jeanne ÉCARNOT** — nom illisible sur la vue de Marnay ; ne rien inventer.
- **[Mamet]**, **[Huot]**, **[Robichon]** — témoins et maire d'Ancier en 1810.
- **[Freyler]** — le juge militaire déclarant en 1890. **rue [Régny]** — domicile de Jeanne en 1888.
- **Beaumotte[-lès-Montbozon ?]** — lieu de naissance du domestique de 1876.
- **Département du [Doubs]** pour Marnay à la publication de 1809 : Marnay est en Haute-Saône, la mention est probablement une erreur du greffier ou une mauvaise lecture. À signaler, pas à corriger silencieusement.

Deux écarts d'âge **normaux**, à ne pas traiter comme des erreurs : Noël est dit vingt-cinq ans en mai 1809 et vingt-six en septembre 1810 alors qu'il avait vingt-sept ; Anne Pierre est dite vingt ans puis vingt-deux. Les âges déclarés de cette époque sont approximatifs et ces flottements d'un an sont l'ordinaire.

Enfin, la correction d'intendance signalée au patch précédent et non encore faite : la naissance de **Joseph Alexandre MONJEAN** est portée au 23 décembre 1844 dans l'encart et le corps de la transcription, et au 24 dans l'en-tête, l'entrée ACTES et le journal de la treizième séance. Naissance le 23, acte le 24 — harmonise en ce sens.
