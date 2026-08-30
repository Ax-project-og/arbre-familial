# ARBRE GÉNÉALOGIQUE — BRANCHE MATERNELLE
# MODIF 30/08 (soir) — Autrey 1811, les naissances de Gray, et un onglet Carte

*Le mariage qui ouvre la génération −1 des PAUFARD · Cinq naissances de Gray dépouillées · Une hypothèse neuve sur la fratrie de Thomas · Une demande de fond : la carte*

---

## 0. Contexte — ce que fait ce patch

Claude, ce patch a trois parties inégales.

**La première est la plus importante du dossier depuis plusieurs séances.** Le mariage de **Jean-Baptiste PAUFARD et de Denise REDOUTET**, célébré **à Autrey-lès-Gray le 13 février 1811**, a été retrouvé. C'était l'un des trois ou quatre actes que le dossier cherchait depuis le début, et il livre exactement ce qu'on en attendait et davantage : **quatre ascendants nouveaux**, la date de naissance exacte des deux époux, le lieu de naissance de Jean-Baptiste — **Gray, et non Oyrières** —, un frère, et surtout **l'explication du métier et de l'installation à Fahy**. Le dossier tenait pour acquis que les décès du couple étaient « la seule voie connue vers la génération −1 des PAUFARD » : cette voie était fausse, c'était le mariage. Voir §1 et §6.4.

**La deuxième est le dépouillement des cinq naissances GRILLOT de Gray** que le patch précédent avait mises en P2. Le résultat est net : **Christine (1834) et Alfred Nicolas (1842) sont de Thomas et de Jeanne**, Françoise Adélaïde (1833) et Anne Louise (1842) ne le sont pas, et Joseph (1835) est maintenant lu sur le registre original et non plus sur un extrait. La fratrie de Napoléon se ferme par les deux bouts, et l'acte d'Anne Louise fait apparaître **une huitième maison GRILLOT à Gray** — qui pourrait bien ne pas être une maison étrangère du tout. Voir §2, §4 et §7.

**La troisième est une demande du propriétaire du dossier.** Il veut un **onglet « Carte »**, centré sur le pays graylois, où toute l'histoire tient dans un carré de trente kilomètres de côté. C'est le §8, et c'est un travail d'affichage : la géographie de ce dossier est un fait, elle n'est nulle part montrée.

---

## 1. La génération −1 des PAUFARD et des REDOUTET

Le mariage d'Autrey nomme quatre parents, tous les quatre vivants, présents et consentants en février 1811. C'est la première fois que le dossier atteint cette génération de ce côté.

### 1.1 — Les quatre fiches à créer

```js
{id:"jean-paufard", prenoms:"Jean", nom:"PAUFARD", gen:1,
 w:270, h:200, small:true, neuf:true, apports:["Nouveau"],
 naissance:{date:"dates à établir", approx:true},
 deces:{date:"après février 1811", approx:true},
 metiers:[{quoi:"propriétaire, Oyrières", an:1811}],
 lieux:[{quoi:"Gray", an:1788, note:"son fils y naît"},
        {quoi:"Oyrières", an:1811}],
 notes:[
   {b:"<b>Présent et consentant au mariage de son fils</b>, en février 1811, et "
     +"<b>signataire</b> — il sait écrire. Propriétaire à Oyrières, il y a auprès de lui un "
     +"aîné, <b>Jean Claude</b>, marchand. C'est le premier PAUFARD que le dossier atteigne."
     +"<span class=\"tag-new\">Nouveau</span>", ferme:true},
   {b:"<b>Sa famille n'est pas d'Oyrières.</b> Son fils Jean-Baptiste naît <b>à Gray</b> le "
     +"17 août 1788 ; en 1811 le ménage est à Oyrières. Le déplacement se place donc entre "
     +"1788 et 1811, et <b>c'est à Gray qu'il faut chercher son propre mariage</b>, vers "
     +"1770-1772 si l'on se règle sur l'aîné.", ferme:false}
 ],
 dossier:[{type:"m", libelle:"Mariage de son fils<span class=\"tag-new\">Nouveau</span>"},
          {type:"x", libelle:"Acte propre non retrouvé"}]},

{id:"francoise-bruyere", prenoms:"Françoise", nom:"BRUYÈRE", f:true, gen:1,
 w:250, h:200, small:true, neuf:true, apports:["Nouveau"],
 naissance:{date:"dates à établir", approx:true},
 deces:{date:"après février 1811", approx:true},
 lieux:[{quoi:"Oyrières", an:1811}],
 divers:[
   {dt:"Signature", dd:"« <b>F. Bruyer</b> » — elle signe, sans l'accent final"}
 ],
 notes:[
   {b:"<b>Elle sait écrire, et sa belle-fille non.</b> À l'acte de 1811, la mère du marié "
     +"signe de sa main tandis que la mariée et la mère de la mariée déclarent l'une et "
     +"l'autre ne savoir le faire. C'est un renseignement social autant qu'un détail de plume."
     +"<span class=\"tag-new\">Nouveau</span>", ferme:true}
 ],
 dossier:[{type:"m", libelle:"Mariage de son fils<span class=\"tag-new\">Nouveau</span>"},
          {type:"x", libelle:"Acte propre non retrouvé"}]},

{id:"francois-redoutet", prenoms:"François", nom:"REDOUTET", gen:1,
 w:290, h:220, small:true, neuf:true, apports:["Nouveau"],
 naissance:{date:"dates à établir", approx:true},
 deces:{date:"après février 1811", approx:true},
 metiers:[{quoi:"<b>maître tailleur de pierre</b>, Fahy", an:1811, neuf:"Nouveau"},
          {quoi:"propriétaire, Fahy", an:1811}],
 lieux:[{quoi:"Fahy-lès-Autrey", an:1811}],
 notes:[
   {b:"<b>C'est lui l'atelier.</b> Le dossier savait depuis les recensements que les PAUFARD "
     +"de Fahy étaient une maison de tailleurs de pierre — quatre fils au même métier sous le "
     +"même toit en 1841 — sans savoir d'où venait le métier. Il vient d'ici : le beau-père "
     +"est <b>maître</b> tailleur de pierre à Fahy, et son gendre, simple tailleur de pierre à "
     +"Oyrières en 1811, vient s'installer chez lui. <b>Jean-Baptiste PAUFARD n'a pas amené le "
     +"métier à Fahy, il y est entré par le mariage.</b><span class=\"tag-new\">Nouveau</span>",
    ferme:true},
   {b:"Il signe, et l'acte porte à côté de sa signature une seconde main, « <b>A. Redoutet</b> », "
     +"que le texte ne justifie pas. <i>À rapprocher — sans rien conclure — de l'</i>"
     +"<b>Antoine REDOUTET</b><i> adjoint faisant fonctions de maire de Fahy en 1852 et 1854, "
     +"et du </i><b>Joseph REDOUTET</b><i> dit cousin germain par alliance de Françoise AMIOT "
     +"en 1865.</i> La place des REDOUTET à Fahy commence à s'expliquer.", ferme:false}
 ],
 dossier:[{type:"m", libelle:"Mariage de sa fille<span class=\"tag-new\">Nouveau</span>"},
          {type:"x", libelle:"Acte propre non retrouvé"}]},

{id:"denise-deurey", prenoms:"Denise", nom:"[DEUREY]", f:true, gen:1,
 w:250, h:200, small:true, neuf:true, doute:true, apports:["Nouveau"],
 naissance:{date:"dates à établir", approx:true},
 deces:{date:"après février 1811", approx:true},
 lieux:[{quoi:"Fahy-lès-Autrey", an:1811}],
 divers:[
   {dt:"Lecture", dd:"le patronyme est <b>incertain</b> : la main de l'officier d'Autrey donne "
     +"quelque chose comme <i>Deurey</i> ou <i>Deures</i>. <b>Ne pas le durcir</b> tant qu'un "
     +"second acte ne l'a pas confirmé"},
   {dt:"Prénom", dd:"sa fille porte son prénom — <b>deux Denise de suite</b>"}
 ],
 notes:[
   {b:"Illettrée : l'acte de 1811 précise que ni la mariée ni sa mère n'ont su signer, quand "
     +"les quatre autres parents et témoins l'ont fait.<span class=\"tag-new\">Nouveau</span>",
    ferme:true}
 ],
 dossier:[{type:"m", libelle:"Mariage de sa fille<span class=\"tag-new\">Nouveau</span>"},
          {type:"x", libelle:"Acte propre non retrouvé"}]}
```

### 1.2 — Les deux unions

```js
{id:"u-paufard-bruyere", epoux:["jean-paufard", "francoise-bruyere"],
 enfants:["jean-baptiste-paufard-1788"], mariage:null, statut:"établie"},

{id:"u-redoutet-deurey", epoux:["francois-redoutet", "denise-deurey"],
 enfants:["denise-redoutet-1789"], mariage:null, statut:"établie"}
```

### 1.3 — Le problème de place, que je te laisse arbitrer

Je n'ai volontairement mis **ni `x` ni `y`** sur les quatre fiches ci-dessus, parce que je ne peux pas les poser sans casser ton tracé.

L'état des lieux : la bande `gen:1` est occupée de `x:170` à `x:1410` par AMIOT / BERTAULT / RENEVIER / PETITOT, puis de `x:1490` à `x:2760` par le bloc GRILLOT. Les quatre nouvelles fiches devraient se placer **au-dessus de leurs enfants**, c'est-à-dire entre `x:930` et `x:1540` — où il n'y a pas un pixel de libre, et où RENEVIER et PETITOT sont déjà eux-mêmes décalés par rapport à leur fille (`barbe-renevier-1774`, en `x:590`).

Deux voies, et **c'est toi qui juges** :

- **décaler tout le bloc GRILLOT** (toutes les fiches de `x ≥ 1490`, aux trois bandes) vers la droite d'environ 1 100 px, en reportant les `bus:` correspondants et en élargissant le canevas ;
- ou **resserrer la bande** : réduire les huit fiches de `gen:1` à `w:220` et rapprocher les colonnes, ce qui libère de la place sans toucher au reste.

La première est propre et coûteuse, la seconde est économique et tasse la mise en page. Le tracé et le moteur sont ton domaine — prends celle des deux que ton `layout()` supporte le mieux, et si tu en vois une troisième, elle sera meilleure que les deux miennes.

**Un détail lié :** dans `GENERATIONS`, la bande `−1` est libellée `≈ 1731 · 1745`. Les quatre nouveaux venus n'ont pas de date, mais ils sont d'une génération sensiblement plus jeune que RENEVIER et PETITOT — leurs enfants naissent en 1788 et 1791. **Ne change pas le libellé tant qu'aucune date n'est établie**, mais garde en tête que cette bande couvre maintenant deux réalités différentes.

### 1.4 — Un collatéral nouveau

Dans l'encadré **« Collatéraux relevés dans les actes »**, ajouter :

> **Oncle de Claude Alexis** — **Jean Claude PAUFARD**, **trente-huit ans** en février 1811 *(l'âge est corrigé de trente-sept à trente-huit sur l'acte même)*, **marchand résidant à Oyrières**, **frère de l'époux** et premier témoin à son mariage. Né vers **1772-1773**, il est l'aîné connu de la maison PAUFARD. *Nouveau*

Et, dans le même encadré, les trois autres témoins d'Autrey, qui ne sont pas de la famille mais qui datent le milieu : **Claude GOUGET**, quarante-trois ans, propriétaire ; **Joseph MARMIER**, trente-huit ans, chaudronnier ; **Toussaint GASCARD**, quarante-deux ans, secrétaire de la mairie — tous trois d'Autrey, dits *amis des époux*. *Une ligne suffit pour les trois.*

---

## 2. Les cinq naissances GRILLOT de Gray : le résultat

Le patch précédent posait la question en P2 et prévoyait quatre actes. Il y en a eu cinq, en comptant la reprise de Joseph sur le registre original. Voici le tableau, et il est net.

| Acte | Date | Père | Mère | Verdict |
|---|---|---|---|---|
| n° 127 de 1833 | née 28 sept. 1833 | **François** GRILLOT, manouvrier, 42 ans | **Françoise THÉVENIN**, 34 ans | ❌ pas la nôtre *(déjà transcrit)* |
| n° 26 de 1834 | née **8 février 1834** | **Thomas** GRILLOT, boucher, 23 ans | **Jeanne ESCARNOT**, 22 ans | ✅ **la nôtre — l'aînée** |
| n° 175 de 1835 | né **2 décembre 1835** | **Thomas** GRILLOT, marchand boucher, 25 ans | **Jeanne ESCARNOT**, 25 ans | ✅ **la nôtre** *(registre original)* |
| n° 26 de 1842 | née **7 février 1842** | **Nicolas Louis** GRILLOT, charpentier, 29 ans | **Anne Antoinette BAILLY**, 29 ans | ❌ pas la nôtre — *mais voir §7.3* |
| n° 35 de 1842 | né **16 février 1842** | **Thomas** GRILLOT, marchand boucher, 31 ans | **Jeanne ÉCARNOT**, 30 ans | ✅ **la nôtre** |

**Les âges concordent au mois près dans les trois actes de Thomas** — 23 et 22 en février 1834, 25 et 25 en décembre 1835, 31 et 30 en février 1842 — pour un homme né le 3 septembre 1810 et une femme née le 27 mars 1811. C'est une vérification indépendante des dates du mariage de Marnay, et elle est parfaite. *Aucune réserve à porter sur ces trois rattachements.*

---

## 3. Fiches à corriger

### 3.1 — `jean-baptiste-paufard-1788`

Sa naissance était `≈ 1788-1791` et son lieu supposé Oyrières. Les deux tombent.

```js
 naissance:{date:"17/08/1788", lieu:"Gray", note:"22 ans et demi en février 1811",
            neuf:"Daté"},
 metiers:[{quoi:"tailleur de pierre, Oyrières", an:1811, neuf:"Nouveau"},
          {quoi:"tailleur de pierre", an:1841},
          {quoi:"propriétaire", an:1846}],
 lieux:[{quoi:"Gray", an:1788, note:"il y naît", neuf:"Nouveau"},
        {quoi:"Oyrières", an:1811},
        {quoi:"Fahy-lès-Autrey", an:1824, note:"attesté par deux actes de 1824"}],
 divers:[
   {dt:"Parents", dd:"<b>Jean PAUFARD</b>, propriétaire à Oyrières, et <b>Françoise "
     +"BRUYÈRE</b> — présents et consentants à son mariage, tous deux signataires"
     +"<span class=\"tag-new\">Nouveau</span>"},
   {dt:"Fratrie", dd:"<b>Jean Claude PAUFARD</b>, trente-huit ans en 1811, <b>marchand à "
     +"Oyrières</b>, premier témoin à son mariage — né vers 1772-1773. <i>Le reste de la "
     +"fratrie n'est pas établi.</i><span class=\"tag-new\">Nouveau</span>"},
   {dt:"Mariage", dd:"<b>Autrey-lès-Gray, le 13 février 1811</b>, acte n° 12 — chez la mariée"
     +"<span class=\"tag-new\">Daté</span>"}
 ],
```

Et cette note, qui remplace l'idée que la famille venait d'Oyrières :

```js
   {b:"<b>Il est né à Gray, pas à Oyrières.</b> L'acte de 1811 produit son extrait de "
     +"naissance des registres de la ville de Gray : le 17 août 1788, à vingt-deux ans et "
     +"demi de son mariage. Le dossier le tenait pour un homme d'Oyrières parce qu'il y "
     +"résidait ; il n'y résidait que depuis l'enfance. <b>La maison PAUFARD est graylaise "
     +"avant d'être d'Oyrières</b>, ce qui déplace d'un cran la recherche de la génération "
     +"d'avant.<span class=\"tag-new\">Nouveau</span>", ferme:true},
   {b:"<b>Il entre dans le métier par sa femme.</b> Tailleur de pierre à vingt-deux ans à "
     +"Oyrières, il épouse la fille d'un <b>maître tailleur de pierre de Fahy</b> et vient "
     +"s'établir chez son beau-père — avant 1824, la table décennale l'y trouve. L'atelier de "
     +"quatre fils que le recensement de 1841 montre sous son toit n'est donc pas le sien : "
     +"<b>c'est celui des REDOUTET, repris par un gendre.</b>"
     +"<span class=\"tag-new\">Nouveau</span>", ferme:true}
```

**Note de cohérence :** son âge déclaré au mariage de son fils en 1836 — quarante-huit ans — tombe **exactement** juste pour un homme né en août 1788. Le recensement de 1846 le dit cinquante-cinq quand il en a cinquante-huit : c'est le recensement qui flotte, pas l'acte. *Retire de la fiche la note « 48 ans en 1836, 55 en 1846 », qui servait à borner une date maintenant connue.*

### 3.2 — `denise-redoutet-1789`

L'identifiant reste `denise-redoutet-1789` — **ne le renomme pas**, il est référencé dans `UNIONS` et probablement ailleurs — mais la date change.

```js
 naissance:{date:"04/04/1791", lieu:"Autrey-lès-Gray", note:"19 ans et 10 mois en février 1811",
            neuf:"Datée", reserve:true},
 lieux:[{quoi:"Fahy-lès-Autrey", an:1811, note:"y réside avant son mariage", neuf:"Corrigé"},
        {quoi:"Oyrières", an:1813},
        {quoi:"Fahy-lès-Autrey", an:1824}],
 divers:[
   {dt:"Parents", dd:"<b>François REDOUTET</b>, propriétaire et <b>maître tailleur de "
     +"pierre</b> à Fahy, et <b>Denise [DEUREY <span class=\"q\">?</span>]</b> — présents et "
     +"consentants à son mariage<span class=\"tag-new\">Nouveau</span>"},
   {dt:"Mariage", dd:"<b>Autrey-lès-Gray, le 13 février 1811</b>, acte n° 12 — <b>mineure</b>, "
     +"à dix-neuf ans et dix mois<span class=\"tag-new\">Daté</span>"}
 ],
```

Et la note existante sur Antoine REDOUTET — celle qui dit *« la parenté avec Denise est probable et non établie »* — se réécrit, parce que le paysage a changé :

```js
   {b:"<b>Les REDOUTET sont de Fahy, et elle en est.</b> Son père y est propriétaire et "
     +"maître tailleur de pierre en 1811. L'<b>Antoine REDOUTET</b> adjoint faisant fonctions "
     +"de maire en 1852 et 1854, et le <b>Joseph REDOUTET</b> dit <i>cousin germain par "
     +"alliance de Françoise AMIOT</i> en 1865, cessent d'être des homonymes commodes : ce "
     +"sont selon toute vraisemblance ses neveux ou petits-neveux. <i>La parenté exacte reste "
     +"à établir</i>, mais la question n'est plus de savoir s'il y en a une."
     +"<span class=\"tag-new\">Nouveau</span>", ferme:false},
   {b:"<b>Elle est illettrée, et l'acte le dit deux fois.</b> Ni elle ni sa mère n'ont su "
     +"signer en 1811, quand son père, son mari, son beau-père, sa belle-mère et les quatre "
     +"témoins l'ont tous fait. Vingt-cinq ans plus tard, au mariage de son fils, elle est "
     +"encore <i>présente et consentante</i> sans signer.", ferme:true}
```

**⚠ Une réserve à porter, et elle est importante.** L'acte dit la mariée « résidant au **Fahy-lès-Autrey** » et « née audit **Autrey** le quatre avril mil sept cent quatre-vingt-onze », l'extrait de naissance étant tiré des registres « de cette commune » — celle où l'on marie, Autrey. Or les publications ont été faites **à Autrey et à Oyrières, pas à Fahy**. Deux lectures possibles : ou bien le lieu de naissance est à corriger en Fahy et l'officier a écrit vite, ou bien **les actes de Fahy étaient alors portés au registre d'Autrey**, Fahy n'étant pas encore commune distincte. La seconde hypothèse, si elle se vérifie, a des conséquences sur tout le dossier. Voir §7.5 — j'en fais une recherche à part entière.

Dans la fiche, cela se porte ainsi :

```js
 divers:[
   {dt:"Réserve", dd:"L'acte la dit née « audit <b>Autrey</b> » alors qu'elle réside à "
     +"<b>Fahy</b> et que les publications ne sont faites qu'à Autrey et Oyrières. "
     +"<b>Ne pas trancher</b> : ou le lieu est à corriger en Fahy, ou l'état civil de Fahy "
     +"était tenu à Autrey en 1791. Le registre d'Autrey de 1791 le dira"}
 ],
```

### 3.3 — `thomas-grillot-1810` et `jeanne-escarnot-1810`

Le patch précédent portait sur la fiche de Thomas *« fratrie non établie »* — laisse cette mention, elle reste vraie. Ce qui change, c'est que **les enfants du couple sont maintenant connus**, et cela vaut d'être dans les deux fiches.

Sur les deux, ajoute :

```js
   {dt:"Enfants", dd:"<b>Christine</b>, née le 8 février 1834 · <b>Joseph</b>, né le "
     +"2 décembre 1835 · <b>François</b>, né le 14 février 1837 <i>(table seule)</i> · "
     +"<b>André François Napoléon</b>, né le 29 janvier 1838 · <b>Alfred Nicolas</b>, né le "
     +"16 février 1842 · <b>Joseph Émile</b>, né le 6 avril 1854 — <b>cinq prouvés par acte "
     +"de naissance</b>, tous à Gray<span class=\"tag-new\">Nouveau</span>"}
```

Et sur la fiche de Jeanne seulement, cette note, qui dit ce que la liste ne dit pas :

```js
   {b:"<b>Six enfants sur vingt ans, et un trou de douze au milieu.</b> Cinq naissent entre "
     +"1834 et 1842, à raison d'une tous les deux ans ; puis plus rien jusqu'à Joseph Émile "
     +"en 1854, quand elle a quarante-trois ans. Ce n'est pas la fin de sa fécondité, "
     +"c'est un intervalle au milieu — et la table des naissances de Gray de 1843 à 1852 est "
     +"vide de GRILLOT. <i>Ou le ménage a vécu ailleurs, ou il a perdu des enfants dont on "
     +"n'a pas les actes.</i><span class=\"tag-new\">Nouveau</span>", ferme:false},
   {b:"<b>La même sage-femme dix-neuf ans durant.</b> <b>Toussaine CARDINET</b>, femme de "
     +"Victor Brutus CASSIN, accoucheuse à Gray, déclare elle-même les naissances de Joseph "
     +"en 1835, d'Alfred Nicolas en 1842 et de Joseph Émile en 1854 — trente-cinq ans, "
     +"quarante-deux ans, cinquante-quatre ans, la même femme d'un bout à l'autre. <i>Thomas "
     +"n'est allé lui-même à la mairie que pour Christine, en 1834.</i>"
     +"<span class=\"tag-new\">Nouveau</span>", ferme:true}
```

### 3.4 — `napoleon-grillot-1838`

L'entrée `divers` `dt:"Fratrie"` posée au patch précédent se réécrit entièrement : deux des quatre noms sont maintenant datés par acte, un cinquième apparaît, et un rattachement se fragilise.

```js
   {dt:"Fratrie", dd:"<b>Christine</b>, née le <b>8 février 1834</b>, l'aînée — dix mois après "
     +"le mariage de Marnay ; une Christine GRILLOT meurt à Gray le 17 juillet 1868, à "
     +"trente-quatre ans · <b>Joseph</b>, né le <b>2 décembre 1835</b>, <i>maréchal des logis "
     +"chef au 1<sup>er</sup> chasseurs</i> et témoin à son mariage en 1866, <b>capitaine en "
     +"retraite</b> et déclarant au décès de leur père en 1890, chevalier de la Légion "
     +"d'honneur · <b>François</b>, né le 14 février 1837, connu de la seule table décennale "
     +"et sans doute mort en bas âge · <b>Alfred Nicolas</b>, né le <b>16 février 1842</b> · "
     +"<b>Joseph Émile</b>, né le 6 avril 1854, marchand boucher rue du Marché — "
     +"<b>cinq prouvés par acte de naissance</b> sur six"
     +"<span class=\"tag-new\">Complété</span>"},
```

Et la note « Trois frères, trois voies » du patch précédent se corrige d'une phrase : ils ne sont pas trois mais **cinq au moins, dont une sœur**. Reformule le début en conséquence — le fond de la note (le boucher, l'officier, la diaspora) reste juste.

### 3.5 — Le point qui se fragilise : Alfred Nicolas est-il « Nicolas Eugène » ?

Le patch précédent posait l'hypothèse : *Nicolas Eugène, porté « ≈ 1839 » sans acte, serait l'Alfred Nicolas de 1842, seul candidat plausible.* L'acte est ouvert, et le résultat est **ambigu — il faut le dire, pas le lisser**.

**Pour :** Alfred Nicolas est prouvé fils de Thomas et de Jeanne ; c'est le seul Nicolas des tables de naissances de Gray de tout le siècle ; il n'y a **aucune** naissance GRILLOT à Gray entre 1843 et 1852.

**Contre :** à la naissance de son fils Albert Thomas, en septembre 1874, **Nicolas GRILLOT se déclare trente-cinq ans**, ce qui le fait naître vers 1839. Alfred Nicolas en aurait eu **trente-deux**. Trois ans d'écart sur sa propre déclaration, c'est beaucoup. Et le dossier l'appelle *Nicolas **Eugène***, quand l'acte de 1842 donne ***Alfred** Nicolas*.

**Conduite à tenir :** garde le rattachement, mais **passe-le de « prouvé » à « probable »** et écris la réserve. Dans l'encadré des collatéraux, la ligne devient :

> **Nicolas GRILLOT** — probablement l'**Alfred Nicolas** né à Gray le **16 février 1842**, fils prouvé de Thomas et de Jeanne : c'est le seul Nicolas des tables, et aucune naissance GRILLOT n'est enregistrée à Gray de 1843 à 1852. **Mais il se déclare trente-cinq ans en septembre 1874**, ce qui en ferait un homme de 1839, et le dossier le connaît sous le prénom d'Eugène et non d'Alfred. *Marchand de bétail puis négociant à Gray, marié à Thérèse POURCELOT, dit « oncle paternel » de Joséphine en 1892 — la parenté, elle, est prouvée ; c'est la date de naissance qui ne l'est pas.* **À trancher**

C'est le genre de nuance qui fait la différence entre un dossier sérieux et un dossier confortable. La recherche qui la résout est au §7.2.

---

## 4. Corrections à apporter à l'existant

### 4.1 — `t-1835-naissance-de-joseph-grillot` : l'original a été retrouvé

L'article existant transcrit un **extrait** délivré pour le service militaire, porté à l'**acte n° 173**. Le registre original de Gray a été ouvert : c'est l'**acte n° 175**, du **4 décembre 1835**, et le texte concorde mot pour mot pour tout le reste — 2 décembre à six heures du soir, Thomas vingt-cinq ans, Jeanne vingt-cinq ans.

**Ne crée pas un second article.** Complète celui-ci :

- change la référence en : *Gray — naissances de 1835, **acte n° 175*** ; et ajoute entre parenthèses *« lu sur le registre original ; un extrait délivré pour le service militaire, porté n° 173, figure au dossier Léonore »* ;
- ajoute la puce **Registre original** aux étiquettes ;
- ajoute à la glose :

> **L'original confirme l'extrait, et corrige son numéro.** Le registre de Gray porte cette naissance à l'**acte n° 175 du 4 décembre 1835**, quand l'extrait du dossier militaire l'annonce au n° 173 — deux numéros d'écart, l'erreur d'un copiste. **Le 2 décembre, lui, est confirmé.** Ce qui règle la divergence signalée depuis deux séances : la table décennale de Gray porte un « Joseph, 16 décembre 1835 » qui **ne peut pas être cet acte-ci**, l'acte n° 175 étant du 4. *Ou la ligne de la table a été mal lue, ou elle désigne un autre enfant d'une autre maison — la table étant déjà connue pour porter tantôt la date de l'acte, tantôt celle de la naissance, et pour flotter sur les millésimes.* **La ligne est à revérifier ; le 2 décembre 1835, lui, ne l'est plus.**

Et dans l'encadré **« Collatéraux relevés dans les actes »**, la ligne de Joseph : **supprime le `<span class="q">?</span>` et la parenthèse sur les quatorze jours d'écart**, qui n'ont plus lieu d'être. Le 2 décembre 1835 est acquis sur registre.

### 4.2 — `t-1833-naissance-de-francoise-adelaide-grillot` : deux corrections

La transcription existante est bonne à deux mots près, et sa glose contient une phrase devenue fausse.

- **« Toussaint Fournerot, [serrurier] public »** → lire **« Toussaint Fourneret, écrivain public »**. *Serrurier public* n'existe pas ; *écrivain public* est bien le métier, et il explique sa présence comme témoin à côté d'un père illettré.
- Le témoin lu **[Mouriou]** se signe plutôt **[Mounion]** ou **[Mouniou]** — garde les crochets, mais signale la variante.
- **La glose dit : « ce François pourrait être le père de Thomas ».** C'est **faux depuis l'acte de décès de 1890**, qui donne Thomas fils de Noël, et depuis le mariage de Marnay. Supprime la phrase et remplace-la par : *« Trois François GRILLOT vivent à Gray dans ces années-là, et aucun n'est le père de Thomas — l'acte de 1890 et le mariage de 1833 le donnent fils de Noël. La question est close, et cette maison-ci reste sans lien établi avec la nôtre. »*

### 4.3 — `t-1792-1892-les-grillot-dans-les-tables-decennales-de-gray` : trois lignes fausses

Le dépouillement des actes met en défaut la lecture de la table sur trois points, dans la seule décennie 1833-1842. **Corrige les lignes et dis pourquoi dans la glose** — c'est une leçon de méthode, pas une rectification honteuse.

| La table portait | L'acte donne | Nature de l'erreur |
|---|---|---|
| Françoise Adélaïde, **20** septembre 1833 | acte n° 127 du **30** septembre | chiffre mal lu |
| Anne Louise, 9 février **1840** | acte n° 26 du 9 février **1842** | **millésime** mal lu |
| Joseph, **16** décembre 1835 | acte n° 175 du **4** décembre | à revérifier — voir §4.1 |

Ajoute à la glose de l'article :

> **Trois lignes sur huit étaient fausses dans une seule décennie.** Le dépouillement des actes de 1833 à 1842 a mis en défaut la lecture de la table sur trois points : un jour (20 pour 30 septembre 1833), un **millésime** (1840 pour 1842), et une date encore inexpliquée pour Joseph. L'avertissement de source placé en tête de cet article disait que ces tables donnent tantôt la date de l'acte, tantôt celle de la naissance ; il faut lui en ajouter un second, plus rude — **elles sont aussi mal lues qu'irrégulières**, et un millésime peut sauter de deux ans. *Aucune date de cet article ne doit servir de preuve. Elles servent à savoir où regarder, rien de plus.*

**Et signale en gras dans la liste des naissances 1833-1842** les trois lignes maintenant rattachées à notre foyer : Christine, Joseph et Alfred Nicolas, comme François André Napoléon l'est déjà.

### 4.4 — L'encadré « Les GRILLOT de Gray — au moins sept maisons »

Il y en a **huit**. Change le titre en **« Les GRILLOT de Gray — au moins huit maisons »**, et complète la ligne **« Années 1830 »**, qui en annonce trois de plus, par un quatrième foyer :

> **Nicolas Louis GRILLOT, charpentier** *(né ≈ 1812-1813)*, et **Anne Antoinette BAILLY** *(née ≈ 1812-1813)* — leur fille **Anne Louise** naît le 7 février 1842, **huit jours avant Alfred Nicolas**, fils de Thomas. Un **Nicolas-Louis GRILLOT meurt à Gray le 5 avril 1865**, ce qui est très probablement lui. *Nouveau — mais voir §7.3 : ce n'est peut-être pas une maison étrangère.*

Et complète la ligne **« La nôtre »**, qui s'arrête à Noël, par la génération suivante :

> …Leur fils **Noël** meurt **rue de la Varosse en 1832**, et son fils **Thomas** relève la boutique : six enfants baptisés à Gray entre 1834 et 1854, dont un capitaine et trois bouchers.

### 4.5 — L'encadré « Les PAUFARD de Fahy — la maison du tailleur de pierre »

La ligne **« Les parents »** est à réécrire de fond en comble, et la dernière — « Quatre fils au même métier » — gagne son explication.

> **Les parents** — Jean-Baptiste **PAUFARD**, **né à Gray le 17 août 1788**, tailleur de pierre puis propriétaire, et Denise **REDOUTET**, **née à Autrey le 4 avril 1791** — mariés **à Autrey-lès-Gray le 13 février 1811**, lui résidant à **Oyrières**, elle à **Fahy**. À Fahy dès 1824, vivants au recensement de 1846. *Daté*

> **D'où vient l'atelier** — Le père de Denise, **François REDOUTET**, est **maître tailleur de pierre et propriétaire à Fahy** en 1811. Jean-Baptiste, simple tailleur de pierre à Oyrières, épouse sa fille et vient s'établir chez lui. **Les quatre fils du recensement de 1841 travaillent dans l'atelier de leur grand-père maternel**, pas dans celui de leur père. *Nouveau*

### 4.6 — Le chapeau

La phrase du chapeau qui range les décès de Jean-Baptiste PAUFARD et de Denise REDOUTET parmi « les seuls actes qui nommeraient la génération d'avant » **n'est plus vraie** : leur mariage l'a nommée. Réécris ce segment :

> …le **mariage d'Autrey**, en 1811, ouvre la génération −1 du côté PAUFARD : il nomme **Jean PAUFARD et Françoise BRUYÈRE**, propriétaires à Oyrières, et **François REDOUTET, maître tailleur de pierre à Fahy**, et sa femme **Denise [DEUREY]**. Il donne à Jean-Baptiste une date et un lieu de naissance — **Gray, le 17 août 1788** — et il explique enfin ce que cinq recensements montraient sans le dire : **l'atelier de tailleurs de pierre de Fahy est celui des REDOUTET**, dans lequel un gendre est entré.

Et **retire** les décès du couple de la liste des urgences : ils gardent leur intérêt, mais ce ne sont plus les seules pièces vers la génération d'avant. Ils descendent d'un cran.

---

## 5. Une remarque de méthode, à porter quelque part

Elle vaut mieux qu'une note de bas de page, et je te laisse choisir où — glose de l'article des tables, ou encadré propre.

**Les témoins de Gray sont des employés de la mairie.** Sur les cinq actes dépouillés cette séance, on retrouve : le **greffier de la justice de paix**, le **concierge de la mairie** *(Pierre François BEDEZ en 1825, Nicolas BELLOT en 1842, Jean-Baptiste BERNARD en 1854 — trois hommes, une même fonction)*, le **voyer de la ville**, l'**agent de police**, le **secrétaire adjoint**, l'**écrivain public**, le **caissier de la Caisse d'épargne**. Ce sont des témoins de service, disponibles à l'hôtel de ville. **Conséquence pratique : à Gray, un témoin ne prouve pas une relation.** C'est l'inverse exact de Marnay en 1833 ou d'Autrey en 1811, où les témoins sont le frère, deux cousins et des voisins nommés comme tels.

**Une exception, et elle vaut d'être relevée.** **Pierre Joseph VERPEAUX, agent de police**, déclare le décès de **Noël GRILLOT** en février 1832 — l'acte le dit expressément **« ami du défunt »**, à quarante-neuf ans. **Deux ans plus tard, à cinquante et un ans, il est témoin à la naissance de Christine**, la première fille de Thomas. Il est employé municipal, donc témoin commode ; mais l'acte de 1832 avait pris la peine de dire qu'il était l'ami. *Le voir revenir à la maison du fils deux ans après avoir enterré le père n'est peut-être pas un hasard de couloir.*

---

## 6. Les transcriptions nouvelles

Quatre articles. Pense à créer pour chacun **l'entrée correspondante dans l'index des actes** (`{id:"a-…", type, titre, date, an, tr, mentions:[…]}`) et à tenir les `dossier:[…]` des fiches en accord avec les `mentions`, sans quoi l'audit de cohérence des fiches signalera l'écart.

### 6.1 · `t-1834-naissance-de-christine-grillot`

**Naissance de Christine GRILLOT** — 8 février 1834 — *Gray — naissances de 1834, acte n° 26* — étiquettes : Acte de naissance · Filiation prouvée
**Placement :** section VI, entre le mariage de Marnay (avril 1833) et la naissance de Joseph (décembre 1835).
**`mentions`** : `thomas-grillot-1810` (principal), `jeanne-escarnot-1810` (principal).

> L'an mil huit cent trente-quatre, le **dix** du mois de **février** à **onze** heures du **matin**, par-devant nous **maire** de la ville de **Gray** soussigné, officier de l'état civil, est comparu **M. Thomas Grillot, boucher, âgé de vingt-trois ans**, lequel nous a présenté un enfant du sexe **féminin**, **né le huit du mois de février de la présente année, à dix heures du soir, à Gray**, de lui présentant et de **dame Jeanne Escarnot, son épouse, âgée de vingt-deux ans, les deux domiciliés à Gray** ; et auquel enfant il a déclaré donner les prénoms et nom de **Christine Grillot** ; lesdites déclaration et présentation faites en présence de M. **Bonaventure [Disqueux], ex-[tailleur]**, domicilié à Gray, âgé de **quatre-vingts** ans, et **Pierre Joseph Verpeaux, agent de police**, domicilié à Gray, âgé de **cinquante et un** ans, et ont les présentant et témoins signé avec nous le présent acte après lecture.
> *Signé : [Disqueux] — Grillot — Verpeaux — [Huguier], maire*

**Glose :**

> **L'aînée, et elle était sous nos yeux.** Christine GRILLOT naît **dix mois après le mariage de Marnay** — le 10 avril 1833, le 8 février 1834 : la mesure exacte d'un premier enfant. La ligne « Christine, 10 février 1834 » figurait dans la table décennale de Gray depuis le premier dépouillement et avait été laissée de côté, faute de savoir à quelle maison la rattacher. **C'est la troisième fois dans ce dossier qu'une ligne écartée par prudence se révèle être la nôtre.**
> **Les deux âges sont exacts au mois près** — vingt-trois ans pour un homme né le 3 septembre 1810, vingt-deux pour une femme née le 27 mars 1811 —, ce qui vérifie indépendamment les dates données par l'acte de Marnay. Thomas est ici simplement **boucher** ; il sera *marchand boucher* dès l'année suivante. Et c'est la seule des cinq naissances qu'il vient déclarer lui-même : à partir de 1835, c'est la sage-femme qui ira.
> **Le second témoin n'est pas un inconnu.** **Pierre Joseph VERPEAUX, agent de police**, avait déclaré deux ans plus tôt le décès de **Noël GRILLOT**, le père de Thomas, et l'acte le disait alors *ami du défunt*. Il a cinquante et un ans ici, quarante-neuf là : c'est bien le même homme.
> *Une Christine GRILLOT meurt à Gray le 17 juillet 1868, à trente-quatre ans — l'âge exact. L'acte reste à ouvrir, et il dira si elle s'était mariée.*

### 6.2 · `t-1842-naissance-d-alfred-nicolas-grillot`

**Naissance d'Alfred Nicolas GRILLOT** — 16 février 1842 — *Gray — naissances de 1842, acte n° 35* — étiquettes : Acte de naissance · Filiation prouvée
**Placement :** section VI, après la naissance de Napoléon (1838).
**`mentions`** : `thomas-grillot-1810` (principal), `jeanne-escarnot-1810` (principal).

> L'an mil huit cent quarante-deux, le **dix-sept** du mois de **février** à **onze** heures du **matin**, par-devant nous **adjoint** de la ville de **Gray**, soussigné, officier de l'état civil, est comparu **[Toussaine] Cardinot, épouse de Victor Brutus [Cassin], accoucheuse à Gray, âgée de quarante et un ans**, laquelle nous a présenté un enfant du sexe **masculin**, **né le seize du mois de février de la présente année, à trois heures du soir, à Gray**, qu'elle nous a déclaré être **fils légitime de Thomas Grillot, marchand boucher, âgé de trente et un ans, et de dame Jeanne Écarnot son épouse, âgée de trente ans, les deux domiciliés à Gray** ; et auquel enfant elle a déclaré donner les prénoms et nom d'**Alfred Nicolas Grillot** ; lesdites déclaration et présentation faites en présence de M. **Claude Antoine Maréchal, [greffier] de la justice de paix**, domicilié à Gray, âgé de **quarante-sept** ans, et **Nicolas Bellot, concierge de la mairie**, domicilié à Gray, âgé de **soixante-[quatre]** ans, et ont les présentateurs et témoins signé avec nous le présent acte après lecture.
> *Signé : femme [Cassin] née [Cardinot] — Maréchal — [l'adjoint, signature illisible]*

**Glose :**

> **Le dernier enfant du premier groupe.** Cinq naissances entre 1834 et 1842, puis rien pendant douze ans : Alfred Nicolas ferme la série. **Les âges sont de nouveau exacts** — trente et un et trente ans, au mois près.
> **C'est aussi le candidat au titre de « Nicolas Eugène ».** Le dossier connaît un **Nicolas GRILLOT**, marchand de bétail puis négociant à Gray, marié à Thérèse POURCELOT, dit *oncle paternel* de Joséphine en 1892 : la parenté est prouvée, la date de naissance ne l'était pas. Alfred Nicolas est le **seul Nicolas** de toutes les tables de naissances de Gray, et aucune naissance GRILLOT n'y est enregistrée de 1843 à 1852. <span class="warn">Mais en septembre 1874, **Nicolas se déclare trente-cinq ans**, ce qui ferait un homme de 1839, et Alfred Nicolas n'en aurait eu que trente-deux. Trois ans sur sa propre déclaration, et un prénom qui n'est pas le même : le rattachement est **probable, pas prouvé**.</span>
> **Deux fonctionnaires de la mairie pour témoins**, le greffier de la justice de paix et le concierge — comme en 1825 pour l'enterrement du bisaïeul, comme en 1854 pour la naissance du dernier-né. *À Gray, un témoin n'établit pas une relation.*
> *L'âge de la sage-femme est lu « quarante et un » ; elle en déclare trente-cinq en 1835 et cinquante-quatre en 1854, ce qui donnerait quarante-deux en 1842. L'écart d'un an est ordinaire et ne remet pas en cause son identité.*

### 6.3 · `t-1842-naissance-d-anne-louise-grillot`

**Naissance d'Anne Louise GRILLOT** — 7 février 1842 — *Gray — naissances de 1842, acte n° 26* — étiquettes : Acte de naissance · Homonyme à écarter
**Placement :** immédiatement avant l'article précédent — les deux actes sont séparés de huit jours et se lisent ensemble.
**`mentions`** : aucune.

> L'an mil huit cent quarante-deux, le **neuf** du mois de **février** à **onze** heures du **matin**, par-devant nous **adjoint** de la ville de **Gray**, soussigné, officier de l'état civil, est comparu **Nicolas Louis Grillot, charpentier, âgé de vingt-neuf ans**, lequel nous a présenté un enfant du sexe **féminin**, **né le sept du mois de février de la présente année, à cinq heures du matin, à Gray**, de lui présentant et de **Dame Anne Antoinette Bailly, son épouse, âgée de vingt-neuf ans, les deux domiciliés à Gray** ; et auquel enfant il a déclaré donner les prénoms et nom d'**Anne Louise Grillot** ; lesdites déclaration et présentation faites en présence de M. **Jean-Baptiste [Rivée], tailleur d'habits**, domicilié à Gray, âgé de **quarante-deux** ans, et **Jean Claude Dupré, huissier**, domicilié à Gray, âgé de **cinquante-cinq** ans, et ont les présentant et témoins signé avec nous le présent acte après lecture.
> *Signé : [illisible] — Grillot — [deux signatures]*

**Glose :**

> **Une huitième maison GRILLOT à Gray**, et la plus troublante de toutes. **Nicolas Louis GRILLOT, charpentier**, né vers 1812-1813, et **Anne Antoinette BAILLY**, du même âge : le métier n'est pas celui de la nôtre, et rien dans l'acte ne les y rattache. **Deux naissances GRILLOT à huit jours d'écart** en février 1842 — exactement le genre d'arithmétique qui a servi à ce dossier pour prouver la pluralité des foyers.
> <span class="warn">**Mais l'écarter serait aller trop vite, et cette fois dans l'autre sens.** Nicolas Louis est né vers 1812-1813 et **ne figure dans aucune table de naissances de Gray** — pas plus que Thomas, né en 1810, dont on sait maintenant qu'il est né à **Ancier**. Or Noël GRILLOT était **boucher à Ancier en 1810** et n'est revenu à Gray qu'ensuite. Un second fils né à Ancier vers 1812-1813 tomberait exactement dans cette fenêtre. Et Thomas nomme son fils de 1842 **Alfred Nicolas**, huit jours après la naissance de la fille d'un Nicolas Louis.</span> *Rien de tout cela n'est une preuve — le prénom Nicolas ne se retrouve nulle part ailleurs dans la lignée, et un charpentier n'est pas un boucher. Mais l'hypothèse est trop bien formée pour être passée sous silence : voir la recherche ouverte.*
> **Cet acte corrige aussi la table décennale**, qui portait cette naissance au **9 février 1840**. Elle est du **9 février 1842**. Le millésime avait sauté de deux ans.

### 6.4 · `t-1811-mariage-de-jean-baptiste-paufard-et-de-denise-redoutet`

**Mariage de Jean-Baptiste PAUFARD et de Denise REDOUTET** — 13 février 1811 — *Autrey-lès-Gray — mariages de 1811, acte n° 12* — étiquettes : Acte de mariage · Filiation · Génération −1 ouverte
**Placement :** section correspondant aux années 1800-1815, avant la naissance de Claude PAUFARD (1813). **C'est la pièce maîtresse de la séance : si l'onglet met en avant les actes décisifs, celui-ci en est un.**
**`mentions`** : `jean-baptiste-paufard-1788` (principal), `denise-redoutet-1789` (principal), `jean-paufard`, `francoise-bruyere`, `francois-redoutet`, `denise-deurey`.

> L'an mil huit cent onze, le **treize février** à **dix** heures du **matin**, par-devant nous **Claude Hubert Roydet, adjoint au maire de la commune d'Autrey-lès-Gray**, pour empêchement du sieur **Léon Charles François [Boisset], maire**, remplissant en l'absence ou empêchement de ce dernier les fonctions d'officier de l'état civil de la commune dudit Autrey, département de la Haute-Saône, ont comparu :
>
> **Jean Baptiste Paufard, âgé de vingt-deux ans et demi, tailleur de pierre, résidant à Oyrières**, département de la Haute-Saône, **né à Gray le dix-sept août mil sept cent quatre-vingt-huit**, comme le constate **l'extrait des registres de naissance de la ville de Gray**, à nous représenté et dûment en forme ; **fils majeur de Jean Paufard, propriétaire, et de Françoise Bruyère, ses père et mère, demeurant audit Oyrières, ici présents et consentants**, d'une part ;
>
> Et **Demoiselle Denise Redoutet, âgée de dix-neuf ans et dix mois, résidant au Fahy-lès-Autrey, née audit Autrey le quatre avril mil sept cent quatre-vingt-onze**, comme le constate l'extrait des registres de naissance de cette commune, à nous représenté ; **fille mineure du sieur François Redoutet, propriétaire et maître tailleur de pierre, et de Denise [Deurey], ses père et mère, demeurant audit Fahy, ici présents et consentants**, d'autre part.
>
> Lesquels nous ont requis de procéder au mariage projeté entre eux, et dont **les publications ont été faites dans les communes d'Autrey et d'Oyrières les trois et dix février présent mois à dix heures du matin**, ainsi qu'il conste par les extraits des registres de publications de promesses de mariage ici représentés ; aucune opposition audit mariage ne nous ayant été signifiée, faisant droit à leur réquisition et après avoir donné lecture de toutes les pièces ci-dessus relatées et du **chapitre six du titre cinq du Code Napoléon, relatif aux droits et devoirs respectifs des époux**, nous avons demandé auxdits futurs époux, et à chacun d'eux séparément, s'ils consentaient à se prendre pour mari et pour femme ; chacun d'eux ayant répondu séparément et affirmativement, **nous leur avons déclaré au nom de la loi que Jean Baptiste Paufard et Denise Redoutet sont unis en mariage**.
>
> De quoi avons dressé acte, en présence du sieur **Jean Claude Paufard, âgé de trente-huit ans, marchand résidant à Oyrières, frère de l'époux** ; de **Claude [Gouget], âgé de quarante-trois ans, propriétaire** ; de **Joseph Marmier, âgé de trente-huit ans, chaudronnier** ; et de **Toussaint Gascard, âgé de quarante-deux ans, secrétaire de la mairie** ; tous demeurant audit Autrey, amis des époux ; qui ont signé avec nous le présent acte, ainsi que **François Redoutet, père de l'épouse**, **Jean Paufard et Françoise Bruyère, père et mère de l'époux**, et **l'époux** — **et non l'épouse, ni sa mère**, qui ont déclaré ne savoir le faire.
> *Signé : Paufard — Paufard — F. Bruyer — [A.] Redoutet — [F.] Redoutet — [Gouget] — J. Marmier — Gascard — Roydet, adjoint*

**Glose :**

> **L'acte que le dossier cherchait sans savoir qu'il le cherchait.** Toutes les séances récentes tenaient les décès de Jean-Baptiste PAUFARD et de Denise REDOUTET pour « la seule voie connue vers la génération −1 des PAUFARD ». Ce n'était pas vrai : leur mariage la donne entière, et il était accessible. **Quatre ascendants nouveaux d'un coup** — Jean PAUFARD et Françoise BRUYÈRE, propriétaires à Oyrières ; François REDOUTET, maître tailleur de pierre à Fahy, et sa femme Denise. Les quatre sont vivants, présents et consentants.
> **Deux dates de naissance exactes.** Jean-Baptiste est **né à Gray le 17 août 1788**, ce que confirme l'arithmétique de l'acte lui-même — vingt-deux ans et demi au 13 février 1811 — et, vingt-cinq ans plus tard, l'âge de quarante-huit ans qu'il déclare au mariage de son fils. **Le dossier le croyait d'Oyrières : il est graylais.** Denise est **née le 4 avril 1791**, mineure de dix-neuf ans et dix mois, d'où le consentement de ses parents.
> **Et l'atelier de Fahy s'explique enfin.** Cinq recensements montraient une maison de tailleurs de pierre sans dire d'où venait le métier ; on l'attribuait au père. Il vient de la belle-famille : **François REDOUTET est *maître* tailleur de pierre à Fahy**, et son gendre, simple ouvrier du métier à Oyrières, vient s'établir chez lui — la table décennale l'y trouve dès 1824. **Les quatre fils de 1841 travaillent dans l'atelier de leur grand-père maternel.** Du même coup, la présence des REDOUTET à Fahy tout au long du siècle — Antoine, adjoint faisant fonctions de maire en 1852 et 1854 ; Joseph, cousin germain par alliance en 1865 — cesse d'être une coïncidence de patronyme.
> **Qui signe, et qui ne signe pas.** Sept des neuf signent, y compris **Françoise BRUYÈRE**, la mère du marié. **Les deux qui ne savent pas sont la mariée et sa mère** — dans la maison du maître artisan, ce sont les femmes qui n'écrivent pas ; dans celle du propriétaire d'Oyrières, elles écrivent. *Denise ne signera pas davantage au mariage de son fils, vingt-cinq ans plus tard.*
> <span class="warn">**Une réserve à ne pas dissoudre.** L'acte dit la mariée résidant **au Fahy** et née **« audit Autrey »**, l'extrait venant des registres « de cette commune », et les publications n'ont eu lieu qu'à **Autrey et Oyrières**, jamais à Fahy. Ou l'officier a écrit vite et elle est née à Fahy ; ou **l'état civil de Fahy était alors tenu à Autrey**. La seconde hypothèse expliquerait plusieurs recherches infructueuses et se vérifie en une vue : le registre d'Autrey de 1791.</span>
> *Deux lectures restent ouvertes : le patronyme de la mère de la mariée, lu **[Deurey]**, et la signature **« A. Redoutet »** que le texte de l'acte ne justifie pas.*

---

## 7. Onglet Recherches

### 7.1 — À passer en « résolues »

> **Où et quand Jean-Baptiste PAUFARD a-t-il épousé Denise REDOUTET ?** — dossier `grillot-paufard`. **À Autrey-lès-Gray, le 13 février 1811**, acte n° 12 — chez la mariée, qui résidait à Fahy. L'acte donne **quatre ascendants nouveaux**, les dates de naissance exactes des deux époux, le lieu de naissance de Jean-Baptiste — **Gray**, et non Oyrières —, un frère aîné, et l'origine de l'atelier de tailleurs de pierre de Fahy. `piece: a-1811-mariage-de-jean-baptiste-paufard-et-de-denise-redoutet`

> **Les quatre naissances GRILLOT de Gray de 1833 à 1842 : lesquelles sont de Thomas ?** — dossier `grillot-paufard`. **Deux sur quatre : Christine, née le 8 février 1834, et Alfred Nicolas, né le 16 février 1842.** Françoise Adélaïde est de François GRILLOT et de Françoise THÉVENIN ; Anne Louise, de **Nicolas Louis GRILLOT, charpentier, et d'Anne Antoinette BAILLY** — une huitième maison. La fratrie de Napoléon compte désormais **six enfants, cinq prouvés par acte**, et **Christine en est l'aînée**. `piece: a-1834-naissance-de-christine-grillot`

> **La date de naissance de Joseph GRILLOT, le capitaine.** — dossier `grillot-paufard`. **Le 2 décembre 1835**, confirmé sur le **registre original de Gray, acte n° 175 du 4 décembre**. La divergence avec le « 16 décembre » de la table décennale se résout contre la table. *Reste à savoir ce qu'est ce 16 décembre.* `piece: a-1835-naissance-de-joseph-grillot`

**Et une recherche à requalifier, pas à résoudre :** l'entrée `deces-jean-baptiste-paufard-denise-redoutet` reste **à faire**, mais sa justification change. Réécris son `pourquoi` : leurs actes ne sont plus *« la seule voie connue vers la génération −1 des PAUFARD »* — cette génération est ouverte. Ils servent maintenant à **dater la fin du couple** et à savoir **où** ils sont morts, ce qui reste utile mais n'est plus stratégique. **Passe-la de P2 à P3.**

### 7.2 — À ajouter, en priorité 1

> **P1 — Le décès de Nicolas Louis GRILLOT, charpentier, à Gray le 5 avril 1865.** `grillot-paufard`
> **Où :** Gray, décès de 1865 — la ligne « Nicolas-Louis, 5 avril 1865 » figure à la table décennale 1863-1872.
> **Pourquoi :** **c'est l'acte le plus rentable ouvert par cette séance.** Un acte de décès nomme les parents du défunt. Si Nicolas Louis, né vers 1812-1813, est dit **fils de Noël GRILLOT et d'Anne Pierre BERNARDOT**, alors la « huitième maison GRILLOT de Gray » n'en est pas une : c'est **le frère de Thomas**, et la fratrie de Thomas — entièrement inconnue à ce jour — s'ouvre par son cadet. S'il est fils d'un autre, la maison est étrangère et l'affaire est classée. **Une vue tranche une question ouverte depuis le début du dossier.**

> **P1 — Le mariage de Nicolas GRILLOT et de Thérèse POURCELOT, avant novembre 1872.** `grillot-paufard`
> **Où :** Gray d'abord, mariages 1860-1872 ; puis les communes voisines si la mariée n'est pas d'ici.
> **Pourquoi :** **c'est le seul acte qui donnera sa date de naissance exacte**, et donc qui dira s'il est ou non l'**Alfred Nicolas** né le 16 février 1842. Trois ans séparent l'âge qu'il déclare en 1874 de celui qu'aurait Alfred Nicolas ; le prénom diffère aussi. Tant que ce mariage n'est pas lu, le rattachement reste **probable et non prouvé**, et il faut l'écrire ainsi partout.

### 7.3 — À ajouter, en priorité 2 et 3

> **P2 — Le décès de Christine GRILLOT, à Gray le 17 juillet 1868.** `grillot-paufard`
> **Où :** Gray, décès de 1868 ; la ligne est à la table décennale 1863-1872.
> **Pourquoi :** l'âge concorde exactement — trente-quatre ans pour une femme née le 8 février 1834. L'acte confirmera qu'il s'agit bien de l'aînée de Thomas et de Jeanne, et **dira si elle s'était mariée** : une sœur mariée de Napoléon signifierait une descendance collatérale entière, jusqu'ici invisible.

> **P2 — Le mariage de Jean PAUFARD et de Françoise BRUYÈRE, à Gray, vers 1770-1775.** `grillot-paufard`
> **Où :** registres paroissiaux de **Gray** — le fils cadet y naît en 1788, l'aîné Jean Claude vers 1772-1773. Chercher aussi les **naissances PAUFARD à Gray entre 1770 et 1795**, qui donneront la fratrie complète.
> **Pourquoi :** c'est la porte de la génération −2 côté PAUFARD, et elle vient de s'ouvrir. Jean-Baptiste étant né à Gray, le couple y était établi en 1788 ; il faut savoir depuis quand, d'où il venait, et combien d'enfants il a eus. **C'est désormais la branche la moins profonde du dossier, et la plus facile à creuser.**

> **P2 — Les REDOUTET de Fahy : la maison du maître tailleur de pierre.** `grillot-paufard`
> **Où :** naissances de **Fahy** (ou d'Autrey, voir ci-dessous) entre 1785 et 1800 pour la fratrie de Denise ; puis le mariage de François REDOUTET avec Denise [DEUREY], vers 1785-1790 ; puis l'identification d'**Antoine REDOUTET**, adjoint faisant fonctions de maire en 1852-1854, et de **Joseph REDOUTET**, quarante-trois ans en 1865.
> **Pourquoi :** trois REDOUTET traversent le dossier sans qu'on sache comment ils s'articulent, et l'on sait maintenant que la famille tient à Fahy un atelier et des biens. **Le lien entre les trois est presque certainement un lien de sang** : le nommer donnerait à la branche maternelle son premier réseau local documenté. *Et le patronyme de la mère de Denise, lu [DEUREY], sera confirmé ou corrigé du même coup.*

> **P3 — Le « Joseph, 16 décembre 1835 » de la table décennale de Gray.** `grillot-paufard`
> **Où :** Gray, naissances de décembre 1835, actes postérieurs au n° 177.
> **Pourquoi :** notre Joseph est à l'acte n° 175 du 4 décembre. Ou la ligne de la table est mal lue, ou **un troisième GRILLOT naît à Gray en décembre 1835** — après Joseph le 2 et Anne Baptiste le 8. Trois naissances en seize jours seraient un argument de plus sur la pluralité des maisons. *Question d'hygiène, pas d'enjeu.*

### 7.4 — Négatives et rectifications

> **La table décennale des naissances de Gray, 1833-1842, est fausse sur trois lignes.** Le dépouillement des actes a corrigé : Françoise Adélaïde, **30** et non 20 septembre 1833 ; Anne Louise, **1842** et non 1840 ; Joseph, acte du **4** et non du 16 décembre 1835. **Conséquence :** l'avertissement de source de cet article, qui ne portait que sur l'irrégularité des dates *(acte ou naissance selon les lignes)*, doit être doublé — **ces tables sont aussi mal lues qu'irrégulières, et un millésime peut se déplacer de deux ans**. Aucune date qui en soit tirée ne doit servir de preuve, ni servir à établir une absence.

> **L'hypothèse « François GRILLOT, père de Thomas » est définitivement close.** Elle survivait dans la glose de la naissance de Françoise Adélaïde. L'acte de décès de 1890 et le mariage de Marnay donnent tous deux Thomas fils de **Noël**. *À supprimer de la glose, non à nuancer.*

### 7.5 — Une recherche d'un genre nouveau, et elle commande le reste

> **P1 — Fahy-lès-Autrey était-elle commune distincte en 1791 ?** `grillot-paufard`
> **Où :** la notice de Fahy-lès-Autrey dans *Des villages de Cassini aux communes d'aujourd'hui* (EHESS), qui donne l'histoire administrative de chaque commune ; puis, comme vérification directe, **le registre des naissances d'Autrey-lès-Gray de 1791**, où l'on doit trouver ou non la naissance de Denise REDOUTET au 4 avril.
> **Pourquoi :** l'acte de 1811 dit la mariée **résidant à Fahy** et **née « audit Autrey »**, son extrait de naissance venant des registres de la commune où l'on marie, et **les publications n'ont été faites qu'à Autrey et Oyrières**, jamais à Fahy. Si Fahy n'était pas encore commune distincte, **tous les actes de Fahy antérieurs à sa création sont au registre d'Autrey** — et plusieurs recherches menées « à Fahy » sur des dates anciennes ont pu échouer pour cette seule raison. <span class="warn">**C'est une question de méthode qui conditionne d'autres recherches, pas une curiosité.** Elle se règle en deux vues et il faut la régler tôt.</span>

---

## 8. La demande de fond : un onglet « Carte »

### 8.1 — Ce qui est demandé, et pourquoi

Le propriétaire du dossier veut **un cinquième onglet, « Carte »**, à côté d'Arbre, Frise, Recherches et Transcriptions.

**Le besoin est réel et pas décoratif.** Cette famille tient dans un mouchoir de poche. Gray, Ancier, Vars, Fahy, Autrey, Oyrières, Mont-le-Frânois, Écuelle, Champlitte, Marnay : **tout ce qui compte se passe dans un carré d'une trentaine de kilomètres de côté**, et les alliances suivent la géographie de bout en bout — un boucher de Gray qui va chercher femme chez un confrère de Marnay à vingt-cinq kilomètres, un tailleur de pierre d'Oyrières qui vient s'installer chez son beau-père à Fahy, une famille de Mont-le-Frânois qui descend sur Vars. **Le texte le dit à chaque page ; rien ne le montre.**

### 8.2 — Le principe d'échelle, qui est la vraie contrainte

**Ne fais pas une carte de France.** Une naissance à Lyon, une mort à Annecy et un cordonnier né à Paris ne justifient pas de dézoomer sur six cents kilomètres, ce qui écraserait la zone utile jusqu'à l'illisibilité — c'est exactement ce qu'il faut éviter.

Je propose **trois niveaux**, et tu ajustes :

1. **La carte principale — « le pays graylois ».** Un cadre approximatif de **47,25° à 47,65° de latitude nord** et de **5,35° à 5,85° de longitude est**, soit environ **35 km sur 45**. Il contient Gray, Gray-la-Ville, Arc-lès-Gray, Ancier, Fahy-lès-Autrey, Autrey-lès-Gray, Vars, Oyrières, Mont-le-Frânois, Écuelle, Champlitte, Montarlot-lès-Champlitte et Marnay. **C'est la carte que l'on voit en ouvrant l'onglet.**
2. **Une vue régionale, en second**, couvrant la Haute-Saône, le nord du Jura, le Doubs et l'est de la Côte-d'Or : elle ajoute Besançon, Baume-les-Dames, Trouvans, Dijon, Beaune, Serrigny, Selongey, Champvans-lès-Dole, Peintre, Authume, Vesoul, Langres et Pressigny. Un bouton, un encart, un second onglet interne — comme tu veux.
3. **Les lointains, en simple liste**, sans carte : Paris, Lyon, Nancy, Saint-Mihiel, Mantes-la-Jolie, Saint-Étienne, Annecy, Bourges, Belley, Grosmagny. Une ligne chacun, avec l'événement qui s'y rattache. *Ils n'ont pas besoin d'être situés, seulement mentionnés.*

### 8.3 — L'implémentation, que je te laisse choisir

Deux voies, et je penche pour la première sans te la imposer :

- **Un SVG inline, projection équirectangulaire simple** sur la boîte englobante, avec la Saône tracée grossièrement comme seul repère, les communes en points, les libellés en `var(--sans)`. **Avantage décisif : aucune dépendance externe, le fichier reste unique et autonome, et le rendu reste dans la typographie sobre du document.** Le dessin n'a pas besoin d'être exact au mètre : à cette échelle, les positions relatives suffisent, et elles seules importent.
- **Leaflet + fonds OpenStreetMap**, plus joli et plus juste, au prix d'un CDN externe et d'un rendu qui jurera avec le reste du document.

**Fonctionnellement**, dans l'ordre d'utilité décroissante : cliquer un lieu affiche **les événements qui s'y sont produits**, avec renvoi vers les transcriptions ; un filtre par patronyme — AMIOT, PAUFARD, REDOUTET, GRILLOT, ÉCARNOT, VILLETTE, CARPENTIER — colore les points ; les distances entre communes sont indiquées quelque part, parce que **c'est le chiffre qui rend la lecture parlante** *(Gray–Fahy 12 km, Fahy–Autrey 3 km, Gray–Vars 10 km, Gray–Marnay 25 km, Gray–Oyrières 12 km)*.

### 8.4 — Les lieux, et ce qui s'y est passé

⚠ **Les coordonnées ci-dessous sont approximatives et données pour dégrossir le placement : vérifie-les avant de les figer.** Elles sont assez justes pour poser une carte de repérage, pas pour un usage cartographique sérieux.

**Le noyau — carte principale**

| Lieu | Dépt | lat / lon *(approx.)* | Ce qui s'y passe |
|---|---|---|---|
| **Gray** | 70 | 47,445 / 5,592 | La ville du dossier. Naissance de Jean-Baptiste PAUFARD (1788) ; les GRILLOT bouchers sur la place puis rue de la Varosse et rue du Marché ; six naissances de Thomas et Jeanne ; décès de Pierre Gabriel (1825), de Noël (1832), de Jeanne (1888), de Thomas (1890) |
| **Fahy-lès-Autrey** | 70 | 47,474 / 5,436 | **Le foyer de la ligne pendant tout le XIX<sup>e</sup>.** L'atelier REDOUTET ; PAUFARD × AMIOT 1836 ; treize enfants ; GRILLOT × PAUFARD ; décès de Françoise AMIOT 1878, de Joséphine 1905 ; mariage de 1906 |
| **Autrey-lès-Gray** | 70 | 47,490 / 5,455 | **Mariage PAUFARD × REDOUTET, 13 février 1811** ; l'étude de M<sup>e</sup> MOREAU ; le fils François y vit |
| **Vars** | 70 | 47,522 / 5,490 | Les RENEVIER ; naissance de Françoise AMIOT (1810) ; décès de Claude RENEVIER et Catherine PETITOT (1807), de Barbe RENEVIER (1818), de François AMIOT (1839) |
| **Oyrières** | 70 | 47,545 / 5,600 | Les PAUFARD de 1811 : Jean le père, Jean Claude l'aîné, Jean-Baptiste avant son mariage |
| **Mont-le-Frânois** | 70 | 47,555 / 5,530 | Le berceau AMIOT — baptême de François (1780), les BERTAULT |
| **Ancier** | 70 | 47,408 / 5,572 | **Naissance de Thomas GRILLOT (1810)** ; Noël y est boucher |
| **Marnay** | 70 | 47,286 / 5,770 | Les ÉCARNOT bouchers ; naissance de Noël GRILLOT (1783) et de Jeanne ÉCARNOT (1811) ; **mariage du 10 avril 1833** ; décès de Jean Pierre ÉCARNOT et de Marguerite GARDOT |
| **Champlitte** | 70 | 47,617 / 5,517 | Nicolle BERTAULT ; un Jean-Baptiste AMYOT à trancher |
| Arc-lès-Gray | 70 | 47,460 / 5,570 | La maison Jacques GRILLOT ; Anne Baptiste LÉONARD y naît |
| Gray-la-Ville | 70 | 47,440 / 5,572 | Décès d'Yvonne (1963) |
| Écuelle | 70 | 47,550 / 5,500 | Origine probable des PETITOT |
| Montarlot-lès-Champlitte | 70 | 47,630 / 5,560 | Joseph GACONNET, instituteur, cousin germain |

**La couronne — vue régionale**

Besançon *(25 — 47,238 / 6,024 : la pharmacie CARPENTIER, mort de Julie-Lucie GÉNIN)* · Baume-les-Dames *(25 — 47,353 / 6,360 : naissance de Victor CARPENTIER)* · Trouvans *(25 — 47,420 / 6,400 : les CARPENTIER propriétaires)* · Dijon *(21 — 47,322 / 5,041)* · Beaune *(21 — 47,023 / 4,840 : le jugement de 1897)* · Serrigny *(21 — 47,050 / 4,880)* · Selongey *(21 — 47,590 / 5,180 : les VILLETTE)* · Champvans-lès-Dole *(39 — 47,100 / 5,450 : **l'origine jurassienne des GRILLOT**, lecture incertaine)* · Peintre *(39 — 47,150 / 5,520 : naissance de MONJEAN)* · Le Magny *(70 : Thomas BERNARDOT — **localisation à vérifier**, plusieurs communes de ce nom)* · Vesoul, Langres, Pressigny.

**Les lointains — liste seule**

Paris *(naissance d'Émile Adolphe VILLETTE, 1840)* · Lyon *(naissance d'Yvonne, 1889 ; la reconnaissance de 1892)* · Nancy *(le professeur GÉNIN)* · Saint-Mihiel *(naissance de Julie-Lucie GÉNIN)* · Mantes-la-Jolie · Saint-Étienne *(mariage FONTANA × RIBAUT, 1963)* · Annecy · Bourges *(hôpital militaire)* · Belley *(garnison de MONJEAN)* · Grosmagny *(**Joseph GRILLOT blessé et fait prisonnier, 2 novembre 1870**)*.

### 8.5 — Deux choses à écrire sur la carte elle-même

Une carte muette ne servirait à rien. Deux légendes valent d'y figurer :

> **Tout tient dans trente kilomètres.** De Mont-le-Frânois à Marnay, il y a moins de quarante kilomètres, et six générations n'en sont pas sorties. Les deux seuls apports lointains — les **CARPENTIER** du Doubs et les **VILLETTE** de Paris — entrent tous deux par mariage et tard, au XIX<sup>e</sup> siècle finissant.

> **Les alliances suivent les routes, et les métiers.** Le boucher de Gray va chercher femme chez un confrère de **Marnay**, à vingt-cinq kilomètres, deux générations de suite. Le tailleur de pierre d'**Oyrières** épouse la fille du maître tailleur de pierre de **Fahy** et vient s'installer chez lui. La famille de **Mont-le-Frânois** descend sur **Vars**, puis sur **Fahy**. *Ce ne sont pas des déplacements au hasard : à chaque fois, on épouse le métier autant que la personne.*

---

## 9. Séance, compteur, vigilance

```js
{date:"30/08/2026 · soir", titre:"Dix-huitième séance — Autrey 1811, et les naissances de Gray",
 actes:[
  {grp:"Autrey-lès-Gray"},
  {quoi:"<b>Mariage 1811, acte n° 12</b> — Jean-Baptiste PAUFARD × Denise REDOUTET "
        +"<i>(quatre ascendants nouveaux)</i>"},
  {grp:"Gray — naissances"},
  {quoi:"<b>1834, acte n° 26</b> — Christine GRILLOT, l'aînée"},
  {quoi:"<b>1835, acte n° 175</b> — Joseph GRILLOT, sur le registre original"},
  {quoi:"<b>1842, acte n° 35</b> — Alfred Nicolas GRILLOT"},
  {quoi:"<b>1842, acte n° 26</b> — Anne Louise GRILLOT <i>(huitième maison)</i>"},
  {quoi:"<b>1833, acte n° 127</b> — Françoise Adélaïde GRILLOT <i>(homonyme, relu)</i>"},
  {grp:"Rectifications"},
  {quoi:"<b>Table des naissances 1833-1842</b> — trois lignes fausses sur huit"}
 ]},
```

**Compteur.** Quatre articles nouveaux — Christine 1834, Alfred Nicolas 1842, Anne Louise 1842, mariage d'Autrey 1811 —, la reprise de Joseph 1835 se faisant **dans l'article existant** et ne comptant donc pas pour un de plus. Le chapeau annonce *quatre-vingt-six actes en main, tous transcrits* et l'onglet affiche **86**, mais je compte **84 articles** dans le fichier. **Recompte par le code plutôt qu'à la main**, corrige les deux chiffres ensemble, et vérifie au passage quels sont les deux articles annoncés qui manquent — ou le compteur qui compte deux fois.

**Points de vigilance, à conserver entre crochets.**
**[DEUREY]**, patronyme de la mère de Denise REDOUTET, et la signature **[A. Redoutet]** que le texte de 1811 ne justifie pas · **[Boisset]**, maire d'Autrey, et **[Gouget]**, témoin · le lieu de naissance de Denise, lu **« audit Autrey »** alors qu'elle réside à Fahy — voir §7.5 · **[Disqueux]** et son métier, lu *ex-[tailleur]*, témoin de 1834 · **[greffier]** de la justice de paix et l'âge de **Nicolas Bellot**, lu soixante-[quatre], en 1842 · **[Rivée]**, tailleur d'habits, en 1842 · l'âge de la sage-femme en 1842, lu quarante et un pour quarante-deux attendus · le prénom de **Nicolas GRILLOT**, *Alfred* sur l'acte de 1842 et *Eugène* dans le dossier, **avec trois ans d'écart sur l'âge qu'il déclare en 1874** — c'est la réserve la plus lourde de ce patch, ne la laisse pas se dissoudre en passant · et, toujours en attente, **[Pierrette] ROUGET** et **rue de la [Varosse]**.

**Un dernier mot, qui vaut consigne générale.** Ce patch corrige trois lignes d'une table décennale et un rattachement présenté comme prouvé. Ce n'est pas un accident de séance : **c'est le prix de la vitesse à laquelle ce dossier avance.** Quand tu écris une fiche, distingue toujours ce qui est établi par acte de ce qui est déduit d'une table ou d'un âge déclaré — le lecteur ne peut pas faire la différence si le texte ne la fait pas, et il n'y a rien de plus difficile à défaire, six mois plus tard, qu'une hypothèse écrite au présent de l'indicatif.
