# ARBRE GÉNÉALOGIQUE — BRANCHE MATERNELLE
# MODIF 30/08 — Marnay, Gray, et les fratries

*Le mariage de 1833 · Le décès de Noël GRILLOT · Trois incohérences à réparer · Une demande de fond : les fratries dans les modales*

---

## 0. Contexte — ce que fait ce patch

Claude, ce patch est plus petit que le précédent en volume mais il comporte **une tâche de fond** qui touche potentiellement toutes les fiches. Je la mets au §4 et c'est celle qui compte le plus.

**Deux actes nouveaux, tous deux décisifs pour la branche GRILLOT.** Le mariage de Thomas et de Jeanne, célébré **à Marnay** — chez la mariée, et non à Gray comme on le supposait — donne d'un coup la mère de Jeanne, jusqu'ici illisible sur la vue de 1811, et **trois dates de décès** que le dossier n'avait pas. Le décès de Noël GRILLOT en 1832 complète la génération et lui donne une adresse.

**Trois incohérences relevées sur le site en ligne.** Elles viennent toutes de ce que la campagne GRILLOT a été intégrée sans que les textes anciens soient relus en regard. Aucune n'est grave, les trois sont visibles par un lecteur attentif. §5.

**Et une demande du propriétaire du dossier, qui est structurelle** : les fratries n'apparaissent pas dans les modales. Napoléon GRILLOT a un frère chevalier de la Légion d'honneur, documenté par deux actes, et sa fiche n'en dit rien — il faut ouvrir l'encadré des collatéraux pour l'apprendre. Ce n'est pas normal : **quand une fratrie est documentée, elle appartient à la fiche de la personne**, pas seulement à un encart transversal. Il ne s'agit pas de créer des cartes pour les frères et sœurs, seulement de les mentionner là où on les cherche, avec la pièce qui les prouve.

---

## 1. Une personne nouvelle, un collatéral nouveau

### 1.1 — Marguerite GARDOT

Mère de Jeanne ÉCARNOT, nommée à l'acte de mariage de 1833. Elle se range en `gen:2`, bande **0**, aux côtés de Jean Pierre ÉCARNOT.

```js
{id:"marguerite-gardot", prenoms:"Marguerite", nom:"GARDOT", f:true, gen:2, x:1080, y:569,
 w:230, h:250, neuf:true, apports:["Nouveau"],
 naissance:{date:"dates à établir", approx:true},
 deces:{date:"20/12/1819", lieu:"Marnay"},
 notes:[
   {b:"<b>Jeanne avait huit ans à sa mort.</b> Son nom manquait : la vue de l'acte de "
     +"naissance de 1811 est illisible à l'endroit où la mère est nommée, et c'est l'acte de "
     +"mariage de sa fille, quatorze ans après sa mort, qui le donne enfin."
     +"<span class=\"tag-new\">Nouveau</span>", ferme:true},
   {b:"L'acte de 1833 précise que <b>les aïeuls et aïeules paternels et maternels de Jeanne "
     +"sont décédés</b> — formule obligatoire pour établir qu'aucun ascendant ne pouvait plus "
     +"consentir. Toute la génération au-dessus des ÉCARNOT et des GARDOT était donc éteinte "
     +"avant avril 1833.", ferme:true}
 ],
 dossier:[{type:"x", libelle:"Acte non retrouvé"}]}
```

**L'union à créer**, qui remplace le mécanisme provisoire mis en place au patch précédent pour rattacher Jean Pierre ÉCARNOT à sa fille :

```js
{id:"u-ecarnot-gardot", epoux:["jean-pierre-ecarnot-1779", "marguerite-gardot"],
 enfants:["jeanne-escarnot-1810"], mariage:null, statut:"établie"}
```

Si tu avais posé une entrée `FILIATIONS` ou une union à un seul époux pour Jean Pierre, **retire-la** : le couple est maintenant complet et se traite comme les autres.

### 1.2 — Hubert ÉCARNOT, à ajouter aux collatéraux

Dans l'encadré « Collatéraux relevés dans les actes », nouvelle ligne :

> **Frère de Jeanne** — **Hubert ÉCARNOT**, trente-deux ans en avril 1833, **marchand boucher à Marnay**, premier témoin au mariage de sa sœur et signataire. Né vers 1801. *Nouveau*

Et, dans le même encadré, ajouter au passage les deux autres parents de la mariée nommés en 1833 : **Étienne DROUHARD**, trente ans, marchand tanneur à Marnay, *cousin germain de l'épouse* ; **Jean François GLAURON**, soixante ans, aubergiste, *cousin issu de germain par alliance*. Ce sont les seuls collatéraux ÉCARNOT connus.

---

## 2. Fiches à corriger

### 2.1 — `jeanne-escarnot-1810`

Sa date de naissance était approximative ; elle est maintenant exacte, et vérifiée deux fois — par l'officier de Marnay en 1833, qui dit s'être reporté aux registres de sa propre commune.

```js
 naissance:{date:"27/03/1811", lieu:"Marnay", note:"acte n° 24 de 1811", neuf:"Datée"},
 divers:[
   {dt:"Parents", dd:"<b>Jean Pierre ÉCARNOT</b>, boucher à Marnay, † 1<sup>er</sup> février 1830, "
     +"et <b>Marguerite GARDOT</b>, † 20 décembre 1819<span class=\"tag-new\">Complété</span>"},
   {dt:"Fratrie", dd:"<b>Hubert ÉCARNOT</b>, marchand boucher à Marnay, né vers 1801 — témoin "
     +"à son mariage<span class=\"tag-new\">Nouveau</span>"},
   {dt:"Variante", dd:"<b>ÉCARNOT</b> sur ses actes de 1811, 1833 et 1888 ; ESCARNOT sur "
     +"l'extrait de 1835 seulement"}
 ],
```

Ajoute cette note, qui dit ce que l'acte de 1833 révèle de sa situation :

```js
   {b:"<b>Orpheline des deux côtés à son mariage.</b> Sa mère est morte quand elle avait huit "
     +"ans, son père quand elle en avait dix-huit, et l'acte de 1833 constate que ses quatre "
     +"grands-parents étaient morts eux aussi. À vingt-deux ans, elle se marie sans un seul "
     +"ascendant vivant — ce sont son frère et deux cousins qui l'accompagnent."
     +"<span class=\"tag-new\">Nouveau</span>", ferme:true}
```

### 2.2 — `jean-pierre-ecarnot-1779`

```js
 deces:{date:"01/02/1830", lieu:"Marnay", neuf:"Daté"},
```

Et sa note sur la mère de Jeanne — « le nom de la mère reste à relever », que j'avais laissée ouverte — est à **supprimer** : elle est relevée. Remplace-la par :

```js
   {b:"Il meurt en février 1830, trois ans avant le mariage de sa fille. Sa veuve l'avait "
     +"précédé de dix ans. C'est son fils <b>Hubert</b>, marchand boucher comme lui, qui "
     +"conduit Jeanne à la mairie de Marnay en 1833.", ferme:true}
```

### 2.3 — `noel-grillot-1783`

Sa fenêtre de décès allait de 1810 à 1890. Elle se referme sur un jour.

```js
 deces:{date:"05/02/1832", heure:"8 h", lieu:"Gray", age:"49 ans déclarés",
        note:"en son domicile, rue de la Varosse [?]", neuf:"Daté"},
 metiers:[{quoi:"marchand boucher, Gray", an:1809},
          {quoi:"boucher, Ancier", an:1810},
          {quoi:"marchand boucher, Gray", an:1832, note:"revenu à Gray"}],
```

```js
   {b:"<b>Personne de sa famille ne déclare sa mort.</b> Deux amis s'en chargent — un agent de "
     +"police et un peintre en bâtiments, tous deux quinquagénaires. C'est le même dispositif "
     +"qu'à la mort de son père sept ans plus tôt, où un avoué et le concierge de la mairie, "
     +"voisins, avaient comparu. Chez ces bouchers de Gray, ce sont les hommes de la rue qui "
     +"accompagnent, pas les fils.<span class=\"tag-new\">Nouveau</span>", ferme:true},
   {b:"Il laisse une veuve de quarante-trois ans et un fils de vingt et un. Quatorze mois plus "
     +"tard, Thomas se mariera comme <i>fils de feu Noël Grillot</i>, en produisant cet acte "
     +"même, annexé au registre de Marnay.", ferme:true}
```

**Attention à la marge d'âge :** l'acte le dit *quarante-neuf ans* alors qu'il en avait quarante-huit — né le 29 août 1783, mort le 5 février 1832. C'est l'écart ordinaire, à ne pas traiter comme une contradiction.

### 2.4 — `anne-pierre-bernardot-1789`

Deux apports, et le second n'est pas anodin.

```js
 metiers:[{quoi:"<b>bouchère</b>, Gray", an:1833, neuf:"Nouveau"}],
 deces:{date:"1833-1890", note:"vivante en avril 1833, dite décédée en février 1890",
        neuf:"Resserré"},
```

```js
   {b:"<b>Veuve, elle tient la boutique.</b> Quatorze mois après la mort de Noël, l'acte de "
     +"mariage de son fils ne la désigne pas par son veuvage mais par son métier : "
     +"<i>bouchère, demeurant à Gray</i>. Elle fait le déplacement jusqu'à Marnay, consent, et "
     +"<b>signe de sa main</b> — <i>anne peire Bernardot</i>. C'est la seule femme de cette "
     +"branche dont on ait à la fois une signature et un état."
     +"<span class=\"tag-new\">Nouveau</span>", ferme:true}
```

### 2.5 — `thomas-grillot-1810` et l'union

```js
 divers:[
   {dt:"Parents", dd:"<b>Noël GRILLOT</b>, boucher, † Gray le 5 février 1832, et "
     +"<b>Anne Pierre BERNARDOT</b>, bouchère<span class=\"tag-new\">Complété</span>"},
   {dt:"Mariage", dd:"<b>Marnay, le 10 avril 1833</b>, acte n° 29 — chez la mariée"
     +"<span class=\"tag-new\">Daté</span>"}
 ],
```

Et dans `UNIONS`, l'entrée `u-escarnot-grillot`, qui portait `mariage:null` :

```js
{id:"u-escarnot-grillot", epoux:["jeanne-escarnot-1810", "thomas-grillot-1810"],
 enfants:["napoleon-grillot-1838"],
 mariage:"10/04/1833", an:1833, acte:"Marnay, acte n° 29", statut:"établie", pw:110,
 bus:1138}
```

*Conserve le `bus:1138` existant : c'est un coude de tracé manuel, ne le perds pas en réécrivant la ligne.*

### 2.6 — `marie-josephe-remy`

Une nuance de lecture à porter, sans trancher :

```js
 deces:{date:"après mars 1825", note:"statut incertain en 1832", approx:true},
 divers:[{dt:"Réserve", dd:"L'acte de décès de son fils, en 1832, écrit « fils de feu Pierre "
   +"Gabriel Grillot <b>et</b> Marie Joseph Rémy » — le <i>feu</i> au singulier ne dit pas si "
   +"elle vivait encore. <b>Ne pas conclure.</b>"}],
```

---

## 3. Le nouvel acte, et la ligne des tables à corriger

Dans l'article **« Les GRILLOT dans les tables décennales de Gray »**, la ligne des décès 1822-1832 porte « Noël, 6 février 1832 » sans commentaire, et la glose ne la mentionne pas. Elle doit maintenant être signalée en gras dans la liste, et la glose gagner ceci :

> **Une ligne était sous nos yeux sans qu'on la voie.** Le « Noël, 6 février 1832 » de la table des décès n'appartient pas à une maison voisine : **c'est le nôtre**, le père de Thomas, dont l'acte confirme la date au 5 février. Cette table contient donc **deux ancêtres directs à trois pages d'écart** — Pierre Gabriel en 1825, Noël en 1832 — et l'un et l'autre avaient été écartés au motif que le nom était trop fréquent. C'est l'effet pervers de la règle d'homonymie : à force de se méfier, on jette ce qu'on cherche.

Dans l'encart **« Les GRILLOT de Gray — quatre maisons »**, la ligne « La nôtre » se complète : *Pierre Gabriel × Marie Josèphe RÉMY, sur la place ; leur fils **Noël**, mort rue de la Varosse en 1832.*

---

## 4. La demande de fond : les fratries dans les modales

**Le constat.** Napoléon GRILLOT a un frère engagé volontaire à dix-neuf ans, blessé et fait prisonnier à Grosmagny, chevalier de la Légion d'honneur, qui vient déclarer la mort de leur père en 1890 avec le grade de capitaine en retraite. **Sa fiche n'en dit pas un mot.** L'information existe, elle est prouvée par deux actes, mais elle est rangée dans un encadré transversal du dossier — là où personne ne la cherchera en ouvrant la fiche de Napoléon.

**Le principe à appliquer.** Il ne s'agit pas de créer des cartes pour les frères et sœurs : l'arbre suit la ligne directe et c'est très bien ainsi. Il s'agit de ce qui suit : **toute fratrie documentée doit apparaître dans la modale de la personne concernée, avec la pièce qui l'établit et le degré de certitude.** Un frère prouvé par acte et un frère supposé par une table décennale ne se présentent pas de la même façon.

**La forme.** Le plus simple est une entrée `divers` avec `dt:"Fratrie"`, qui existe déjà et s'affiche sans rien changer au moteur. Si tu préfères créer un bloc `fratrie:[…]` dédié, avec un rendu propre à lui — une petite liste, comme dans les encarts de fratrie —, fais-le : **c'est plus lisible quand il y a plus de trois noms**, et cela permet de distinguer visuellement le prouvé du probable. Mais alors il faut aussi écrire le rendu, et c'est toi qui juges si le jeu en vaut la chandelle. Dans le doute, `divers` suffit.

### 4.1 — Le cas qui a motivé la demande : `napoleon-grillot-1838`

```js
   {dt:"Fratrie", dd:"<b>Joseph</b> GRILLOT, né le 2 décembre 1835 à Gray — <i>maréchal des "
     +"logis chef au 1<sup>er</sup> chasseurs</i> et témoin à son mariage en 1866, "
     +"<b>capitaine en retraite</b> et déclarant au décès de leur père en 1890 ; chevalier de "
     +"la Légion d'honneur · <b>Nicolas Eugène</b>, ≈ 1839-1840, marchand boucher puis "
     +"négociant à Gray, dit <i>oncle paternel</i> de Joséphine en 1892 · <b>Joseph Émile</b>, "
     +"né le 6 avril 1854 à Gray, marchand boucher rue du Marché — les trois <b>prouvés par "
     +"acte</b> · <b>François</b>, né le 14 février 1837, connu de la seule table décennale et "
     +"sans doute mort en bas âge<span class=\"tag-new\">Nouveau</span>"},
```

Et cette note, parce qu'elle dit quelque chose que la liste seule ne dit pas :

```js
   {b:"<b>Trois frères, trois voies.</b> Napoléon reprend le métier et le déplace — boucher à "
     +"Gray, puis marchand de bestiaux à Fahy, où il épouse une propriétaire. Joseph part à "
     +"l'armée à dix-neuf ans et en revient capitaine et décoré. Joseph Émile, le cadet, reste "
     +"boucher rue du Marché et ses quatre fils essaiment vers Nancy et Paris. En une "
     +"génération, la boucherie de Gray produit un notable de village, un officier et une "
     +"diaspora.", ferme:true}
```

### 4.2 — L'audit à mener sur toute la ligne

Voici, fiche par fiche, ce que le dossier sait déjà et qui devrait figurer dans la modale. **Vérifie chacune** : certaines l'ont peut-être déjà, auquel cas il n'y a rien à faire.

| Fiche | Fratrie à porter | Source |
|---|---|---|
| `napoleon-grillot-1838` | Joseph, Nicolas Eugène, Joseph Émile *(prouvés)* ; François *(table)* | mariage 1866, décès 1890, mariage 1892, naissance 1854 |
| `jeanne-escarnot-1810` | **Hubert ÉCARNOT**, marchand boucher | mariage 1833 |
| `claude-alexis-paufard-1813` | Françoise *(épouse CHATEAU)*, François, Jean-Baptiste, Bazile, « François jeune » ; Anne *(probable)* | recensements 1841 et 1846, décès 1865, tables |
| `theolinde-paufard-1843` | douze frères et sœurs — **renvoyer à l'encart** plutôt que recopier | encart de la fratrie |
| `francois-amiot-1780` | Jean-Baptiste, cultivateur ; François Bernard, propriétaire ; **Françoise**, l'aînée | mariage 1803, baptême de 1781 |
| `camille-villette-1877` | Marie Berthe *(† 1875)*, Félix Jean-Baptiste, Ernest, Marie | dépouillement Selongey |
| `victor-carpentier-1856` | **Marie Antoinette Éléonore**, née le 28 mai 1853 à Baume-les-Dames | naissance 1853 |
| `josephine-grillot-1869` | **fille unique** — c'est un résultat de recherche, pas une absence d'information | recherche résolue |
| `yvonne-grillot-1889` | **fille unique** | idem |
| `renee-villette-1908` | **Jean Émile VILLETTE**, qui a sa propre carte | acte |
| `simone-ribaut-1933` | **Françoise RIBAUT**, qui a sa propre carte | papiers de famille |
| `cecile-fontana-1966` etc. | les deux sœurs, qui ont leurs cartes | papiers de famille |
| `thomas-grillot-1810` | **inconnue** — le porter comme tel : *« fratrie non établie ; les naissances GRILLOT d'Ancier et de Gray entre 1811 et 1832 restent à dépouiller »* | — |

Pour les personnes dont les frères et sœurs **ont déjà une carte dans l'arbre** — Renée et Jean Émile, Simone et Françoise, les trois sœurs FONTANA —, une mention brève suffit : le lecteur les voit à l'écran. Pour les autres, c'est la seule trace qu'il en aura.

**Un point de rédaction, et il compte.** Quand une fratrie n'est pas établie, **écris-le**. Une modale qui ne dit rien laisse croire que la personne était enfant unique ; une modale qui dit « fratrie non établie » indique un travail à faire. Les deux se ressemblent à l'affichage et ne signifient pas du tout la même chose.

---

## 5. Trois incohérences relevées sur le site en ligne

Elles viennent toutes de ce que la campagne GRILLOT a été intégrée sans relire en regard les textes plus anciens. Aucune n'est grave ; les trois se voient.

### 5.1 — Deux listes de « quatre » qui ne se recouvrent pas

Le nouvel encart **« Les GRILLOT de Gray — quatre maisons »** nomme : Pierre Gabriel × RÉMY, Jacques × VALLON, Marie Ferréol × PREVOT, Joseph × MARCHAND.

Le paragraphe **« Homonymes à écarter »**, plus ancien, dit de son côté : *« Même situation à Gray, où quatre foyers GRILLOT coexistent dans les années 1830 »* et nomme Thomas × ÉCARNOT, François × THÉVENIN, Jean × LÉONARD, François × PAGE.

**Ce sont deux jeux différents, et le lecteur lit deux fois « quatre ».** La vérité est plus intéressante que l'une ou l'autre : les deux listes ne se recouvrent que par la nôtre, elles décrivent deux époques — le tournant du siècle d'un côté, les années 1830 de l'autre — et **il y a donc au moins sept foyers GRILLOT à Gray entre 1790 et 1840**, dont un seul est le nôtre. Fusionne les deux passages en un seul, chronologique, et donne le bon chiffre. Le titre de l'encart devient **« Les GRILLOT de Gray — au moins sept maisons »**, ce qui est à la fois plus juste et plus dissuasif pour un futur rattachement hâtif.

### 5.2 — Le chapeau et le compteur ne disent pas la même chose

Le chapeau annonce *« soixante-quinze actes en main, dont soixante et onze transcrits »*. L'onglet Transcriptions affiche **84**. Le premier chiffre est resté au patch précédent. Recompte les deux et harmonise — et pense à ce couple de chiffres à chaque patch, c'est le genre de détail qui décrédibilise un dossier par ailleurs sérieux.

*Note au passage : le patch précédent prévoyait 85 transcriptions et le compteur en affiche 84. Vérifie qu'aucun des quatorze articles n'est resté au bord de la route.*

### 5.3 — Quatre gloses devenues fausses ou périmées

Les articles ci-dessous portent encore des questions que les séances suivantes ont refermées.

- **« Les PAUFARD dans les tables décennales de Fahy »** — la glose dit encore : *« Une Françoise PAUFARD meurt le 3 octobre 1865 […] l'acte seul le dira. »* L'acte est ouvert, c'est bien la sœur, et **la date est le 8 octobre, non le 3** : la lecture de la table était fautive. Corrige la ligne dans la liste des décès **et** la glose.
- **« Décès de Bazille Théophile Alphonse PAUFARD »** — la glose dit *« sa naissance vers mars 1841 — l'acte reste à retrouver »*. La table donne l'acte au **30 mars 1841**, donc une naissance le 29. Il n'est plus « le seul enfant de la fratrie dont nous n'ayons que le décès ».
- **« Décès de Gustave François PAUFARD »** — *« sa naissance, vers le 10 octobre 1844, reste à retrouver »* : la table donne l'acte au 9 octobre, donc une naissance le 8, ce qui concorde avec les « environ huit jours » de l'acte de décès.
- **« Naissance de Clotilde Stéphanie Émérite PAUFARD »** — la glose suppose que le prénom est repris parce que l'aînée serait morte, *« peut-être hors de Fahy — piste à vérifier »*. La piste **a été vérifiée** : Clotilde Hortense n'est pas dans les décès de Fahy de 1839, ni dans aucune table de la commune jusqu'en 1872, ni dans aucun des cinq recensements. Reformule : *le prénom est repris alors que l'aînée est vivante quelque part — c'est l'anomalie, et elle reste entière.*

---

## 6. Les deux transcriptions

### 6.1 · `t-1833-mariage-de-thomas-grillot-et-de-jeanne-ecarnot`

**Mariage de Thomas GRILLOT et de Jeanne ÉCARNOT** — 10 avril 1833 — *Marnay — mariages de 1833, acte n° 29* — étiquettes : Acte de mariage · Filiation · Pièces annexées

**Placement :** section VI, entre le décès de Pierre Gabriel (1825) et les pièces de 1854.

> L'an mil huit cent trente-trois, le dix avril à huit heures du matin, par-devant nous **Pierre Demoulin, maire**, officier de l'état civil de la commune de **Marnay, chef-lieu de canton**, département de la Haute-Saône, sont comparus en notre maison commune :
>
> **Thomas Grillot, âgé de vingt-deux ans et demi, né à Ancier le trois septembre mil huit cent dix**, ainsi qu'il est constaté sur son **extrait de naissance qui nous a été ici représenté, lequel sera annexé au présent registre** ; **boucher domicilié à Gray**, majeur, **fils de feu Noël Grillot, décédé à Gray le cinq février mil huit cent trente-deux**, ainsi qu'il est constaté sur son **acte de décès extrait des registres de l'état civil de la ville de Gray, lequel annexé au présent registre** ; **et de Anne Pierre Bernardot, bouchère, demeurant à Gray, ici présente et consentante** audit mariage ;
>
> Et **Jeanne Écarnot, âgée de vingt-deux ans, née à Marnay le vingt-sept mars mil huit cent onze**, ainsi que nous nous le sommes vérifié sur les registres de l'état civil de la commune de Marnay ; **sans état, domiciliée à Marnay, fille majeure de feu Jean Pierre Écarnot, décédé à Marnay le premier février mil huit cent trente**, et de feue **Marguerite Gardot, décédée audit Marnay le vingt décembre mil huit cent dix-neuf**, ainsi que nous nous le sommes vérifié sur les registres de l'état civil de la commune de Marnay ; **ses aïeuls et aïeules paternels et maternels décédés** ;
>
> Lesquels nous ont requis de procéder à la célébration du mariage projeté entre eux, et dont les publications ont été faites, à Marnay devant la principale porte de notre maison commune les dimanches **vingt-quatre et trente et un mars** derniers, et devant la principale porte de l'hôtel de la mairie de la ville de Gray les mêmes dimanches, ainsi qu'il est constaté sur le certificat délivré par **Monsieur Cornut, premier adjoint de la ville de Gray**, lequel certificat sera annexé au présent registre ; aucune opposition audit mariage ne nous ayant été signifiée, ni à Monsieur le Maire de la ville de Gray. Faisant droit à leur réquisition, après avoir donné lecture de toutes les pièces ci-dessus mentionnées et du chapitre six du Code civil intitulé *du mariage*, et avoir demandé au futur époux et à la future épouse s'ils veulent se prendre pour mari et pour femme, chacun d'eux ayant répondu séparément et affirmativement, **déclarons au nom de la loi que Thomas Grillot et Jeanne Écarnot sont unis par le mariage**.
>
> De quoi nous avons dressé acte en présence de **Hubert Écarnot, âgé de trente-deux ans, marchand boucher, frère de l'épouse** ; **Jean François [Glauron], âgé de soixante ans, aubergiste, cousin issu de germain par alliance de l'épouse** ; **Étienne [Drouhard], âgé de trente ans, marchand tanneur, cousin germain de l'épouse** ; et **Pierre Colin, âgé de cinquante-sept ans, secrétaire de la mairie, ami des époux** ; les quatre demeurant à Marnay ; lesquels, après que lecture leur en a été donnée, ont signé avec nous et les parties contractantes, **ainsi que la mère de l'époux**.
>
> *Signé : Jeanne Écarnot — Grillot — Glauron — **anne peire Bernardot** — Étienne Drouhard — Hubert Écarnot — Colin — Demoulin*

**Glose :**

> **L'acte le plus dense de la branche GRILLOT.** Il donne en une page ce que six mois de tables n'avaient pas donné : la **mère de Jeanne**, Marguerite GARDOT, dont le nom était illisible sur la vue de 1811 ; et **trois dates de décès** — Noël GRILLOT à Gray le 5 février 1832, Jean Pierre ÉCARNOT à Marnay le 1<sup>er</sup> février 1830, Marguerite GARDOT à Marnay le 20 décembre 1819. Il donne aussi à Jeanne sa date de naissance exacte, le 27 mars 1811, l'officier ayant vérifié sur ses propres registres.
> **Le mariage se fait chez elle**, à Marnay, et non à Gray. C'est l'usage, mais ici cela redouble un lien qui existait déjà : le père de Thomas était né à Marnay en 1783, et son fils y revient chercher femme cinquante ans plus tard. **Deux générations, deux fois la même commune, et deux fois le métier de boucher** — le père de la mariée l'était, son frère Hubert l'est encore.
> **Deux orphelins.** Thomas a perdu son père quatorze mois plus tôt ; Jeanne a perdu sa mère à huit ans, son père à dix-huit, et l'acte constate en outre que ses quatre grands-parents sont morts. Sur les six ascendants que les deux mariés pouvaient avoir vivants, **un seul l'est** : Anne Pierre BERNARDOT, qui fait le déplacement depuis Gray, consent, et signe de sa main.
> **Et un mot vaut d'être relevé** : elle n'est pas dite *veuve* mais **bouchère**. Quatorze mois après la mort de son mari, elle tient la boutique et l'officier la désigne par son métier.
> *Trois pièces sont dites annexées au registre de Marnay : l'extrait de naissance de Thomas, l'acte de décès de son père, et le certificat de publication délivré par l'adjoint de Gray. Elles y sont peut-être encore.*

### 6.2 · `t-1832-deces-de-noel-grillot`

**Décès de Noël GRILLOT** — 6 février 1832 — *Gray — décès de 1832, acte n° 29* — étiquettes : Acte de décès · Filiation

**Placement :** section VI, entre le décès de Pierre Gabriel (1825) et le mariage de 1833.

> L'an mil huit cent trente-deux, le **six** du mois de **février** à **dix** heures du **matin**, par-devant nous **deuxième adjoint de la ville de Gray** soussigné, officier de l'état civil, sont comparus MM. **Pierre Joseph Verpeaux, agent de police**, domicilié à Gray, âgé de **quarante-neuf** ans, **ami** du défunt ; et **Jean Jacques Mongin, peintre en bâtiments**, domicilié à Gray, âgé de **cinquante-quatre** ans, **aussi ami** du défunt ; lesquels nous ont déclaré que **Noël Grillot, marchand boucher, époux d'Anne Pierre Bernardot, fils de feu Pierre Gabriel Grillot et Marie Joseph Rémy, âgé de quarante-neuf ans, domicilié à Gray, né à Marnay, département de la Haute-Saône, est décédé le cinq du mois de février de la présente année à [huit] heures du matin, en son domicile, rue de la [Varosse]** ; et ont les déclarants signé après lecture le présent acte que nous avons rédigé après nous être assurés du décès.
> *Signé : Mongin — Verpeaux — [Ernest ?], l'adjoint*

**Glose :**

> **La ligne était dans la table depuis le début.** « Grillot — Noël — 6 février 1832 » figure au relevé des décès de la décennie 1823-1832, et elle avait été écartée au motif que le prénom se retrouvait dans la maison Jacques. C'est bien le nôtre, et cette table contient donc **deux ancêtres directs à sept ans d'écart** — Pierre Gabriel en 1825, son fils Noël en 1832. C'est le revers de la règle d'homonymie : à force de se méfier d'un nom fréquent, on écarte ce qu'on cherche.
> Il meurt à **quarante-huit ans** — l'acte en dit quarante-neuf, l'écart ordinaire — et le lieu de naissance confirme **Marnay, Haute-Saône**, ce qui corrige au passage la mention « département du Doubs » portée par erreur sur la publication de 1809.
> **Personne de sa famille ne déclare.** Deux amis, un agent de police et un peintre en bâtiments, tous deux quinquagénaires. Son père était mort dans les mêmes conditions sept ans plus tôt, déclaré par un avoué et le concierge de la mairie, l'un et l'autre voisins. Il faudra attendre 1890 pour qu'un GRILLOT soit déclaré mort par son propre fils — et ce fils-là sera capitaine.
> *La rue est lue « de la Varosse » sous réserve.*

---

## 7. Onglet Recherches

### 7.1 — Résolues

> **Où et quand Thomas GRILLOT a-t-il épousé Jeanne ÉCARNOT ?** — dossier `grillot-paufard`. **À Marnay, le 10 avril 1833**, chez la mariée et non à Gray comme on le cherchait. L'acte donne en outre la mère de Jeanne, sa date de naissance exacte, et trois dates de décès. `piece: a-1833-mariage-de-thomas-grillot-et-de-jeanne-ecarnot`

> **Qui est la mère de Jeanne ÉCARNOT ?** — dossier `grillot-paufard`. **Marguerite GARDOT**, morte à Marnay le 20 décembre 1819. Son nom était porté à l'acte de naissance de 1811 mais la vue est illisible à cet endroit ; c'est le mariage de sa fille, quatorze ans après sa mort, qui l'a livré. `piece: a-1833-mariage-de-thomas-grillot-et-de-jeanne-ecarnot`

> **Quand meurt Noël GRILLOT ?** — dossier `grillot-paufard`. **Le 5 février 1832 à Gray**, à quarante-huit ans, rue de la Varosse. La fenêtre allait de 1810 à 1890. La ligne figurait dans la table décennale des décès et avait été écartée à tort comme homonyme. `piece: a-1832-deces-de-noel-grillot`

> **Le Joseph GRILLOT de la Légion d'honneur est-il de la ligne directe ?** — dossier `grillot-paufard`. **C'est le frère de Napoléon**, donc l'oncle de Joséphine. Deux actes le prouvent : le mariage de 1866, où il est *frère du futur*, et le décès de Thomas en 1890, où il est *capitaine en retraite, cinquante-cinq ans, fils du défunt*. Il n'est pas un ancêtre, mais il est aussi proche qu'un non-ancêtre puisse l'être. `piece: a-1890-deces-de-thomas-grillot`

### 7.2 — Négatives

> **Les tables de successions du bureau de Gray sont inexploitables pour ce dossier.** Cherché pour la succession de Joséphine GRILLOT, morte le 8 septembre 1905. **Conséquence : il n'y a rien entre 1824 et 1944.** Cette lacune ferme d'un coup plusieurs voies que le dossier tenait en réserve — la succession de **Barbe AMIOT** en 1839, celle de **Claude PAUFARD** en 1865, celle de **Françoise AMIOT** en 1878, et surtout le recours aux tables comme moyen de dater les décès de **Jean-Baptiste PAUFARD et Denise REDOUTET**. *À porter aussi dans le paragraphe « Où chercher » du dossier, qui présente encore les tables de successions comme une source inexploitée : elles ne le sont pas, elles sont manquantes.*

> **Clotilde Hortense PAUFARD n'est pas morte l'année de sa naissance.** Cherché dans les décès de Fahy de 1839. **Conséquence :** elle n'est pas morte nourrisson, ce qui restait l'explication la plus simple de son absence du recensement de 1841. Elle a donc bien **quitté le foyer très tôt et vécu ailleurs**. La piste reste entière et se déplace vers les autres ménages de Fahy, puis vers les mariages d'Autrey et de Gray.

> **Aucune naissance GRILLOT à Gray entre 1843 et 1852.** Cherché dans la table décennale. Un *Grillet* y figure, écarté : le père est cordonnier. **Conséquence :** entre **Alfred Nicolas, acte du 17 février 1842**, et **Joseph Émile, né le 6 avril 1854**, il y a **douze ans sans naissance GRILLOT à Gray**. Jeanne ÉCARNOT avait trente et un ans en 1842 et quarante-trois en 1854 : un tel creux au milieu de la période féconde ne se produit pas tout seul. Soit le ménage a vécu ailleurs — **Ancier ou Marnay** sont les deux candidats —, soit les naissances sont enregistrées dans une autre commune. *Voir la recherche P2 ci-dessous.*

> **À corriger — les décès de Jacques et de Joseph GRILLOT.** Le dépouillement des tables de décès de Gray est maintenant complet pour **1802-1812, 1823-1832 et 1833-1842** : ni l'un ni l'autre n'y figure. **Conséquence : il ne reste qu'une fenêtre, la décennie 1813-1822**, dont le bloc GRILLOT n'a jamais été ouvert — celui qui l'avait été par erreur était du **GILLOT**. La recherche n'a donc pas échoué, elle n'a pas encore été faite au bon endroit. *Passe-la de P1 à P2 : elle sert à savoir si les maisons graylaises n'en font qu'une, ce qui est une élégance et non un besoin — la ligne directe est complète jusqu'au Jura sans elle.*

### 7.3 — À faire

> **P2 — Les quatre naissances GRILLOT de Gray de 1833 à 1842 : lesquelles sont de Thomas ?** `grillot-paufard`
> **Où :** Gray, actes de naissance — **Alfred Nicolas, 17 février 1842** en priorité, puis **Anne Louise, 9 février 1840**, **Christine, 10 février 1834**, **Françoise Adélaïde, 20 septembre 1833**.
> **Pourquoi :** trois raisons convergent. **Nicolas Eugène**, frère de Napoléon, est porté « ≈ 1839 » sans acte, et aucun Nicolas ne naît à Gray cette année-là : l'Alfred Nicolas de 1842 est le seul candidat plausible, et son acte tranchera. **Christine**, née dix mois après le mariage de 1833, serait l'aînée de la fratrie si elle est de Thomas — et une Christine GRILLOT meurt à Gray en 1868, à trente-quatre ans. Enfin, **cinq de ces naissances tombent en janvier ou février** sur neuf années, ce qui suggère un même foyer plutôt que deux. Quatre actes suffisent à fermer la fratrie de Napoléon par les deux bouts.

> **P2 — Où étaient Thomas et Jeanne entre 1842 et 1854 ?** `grillot-paufard`
> **Où :** tables décennales des naissances d'**Ancier** et de **Marnay**, 1843-1852 ; à défaut, recensements de Gray de 1846 et 1851.
> **Pourquoi :** douze ans sans naissance enregistrée à Gray au milieu de la vie féconde du couple. Thomas est né à Ancier, sa mère y a vécu, Jeanne est de Marnay : ce sont les deux communes où le ménage a pu se replier. Une réponse positive donnerait plusieurs enfants d'un coup ; une réponse négative ferait de ce creux un fait, et il faudrait alors le lire comme tel.

> **P3 — Naissances GRILLOT à Ancier et à Gray, 1811-1832 : la fratrie de Thomas.** `grillot-paufard`
> **Pourquoi :** sa fratrie est entièrement inconnue. Ses parents se marient en 1809, il naît en 1810, son père meurt en 1832 : il y a vingt-deux ans de vie conjugale à dépouiller, d'abord à Ancier où le ménage s'était établi, puis à Gray où il était revenu avant 1832.

> **P3 — Décès de Marie Josèphe RÉMY et d'Anne Pierre BERNARDOT.** `grillot-paufard`
> **Où :** Gray, décès postérieurs à 1825 pour la première, à avril 1833 pour la seconde.
> **Pourquoi :** ce sont les deux dernières femmes de la branche GRILLOT sans date de mort. Celui d'Anne Pierre nommerait ses parents, Thomas BERNARDOT et [Pierrette] ROUGET, et lèverait le doute sur le prénom de cette dernière.

> **P3 — Mariage Hubert ÉCARNOT, et la descendance ÉCARNOT de Marnay.** `grillot-paufard`
> **Pourquoi :** né vers 1801, marchand boucher, c'est le seul collatéral connu de cette branche. Sa descendance est la seule chance de retrouver un jour des papiers de famille du côté ÉCARNOT.

---

## 8. Séance, compteur, vigilance

```js
{date:"30/08/2026", titre:"Dix-septième séance — Marnay, et le retour sur les tables de Gray",
 actes:[
  {grp:"Marnay"},
  {quoi:"<b>Mariage 1833, acte n° 29</b> — Thomas GRILLOT × Jeanne ÉCARNOT"},
  {grp:"Gray"},
  {quoi:"<b>Décès 1832, acte n° 29</b> — Noël GRILLOT, rue de la Varosse"},
  {quoi:"<b>Tables de décès 1823-1832 et 1833-1842</b> — bloc GRILLOT complet, ni Jacques ni Joseph"},
  {quoi:"<b>Table des naissances 1843-1852</b> — aucune naissance GRILLOT en douze ans"},
  {grp:"Recherches négatives"},
  {quoi:"<b>Successions du bureau de Gray</b> — rien entre 1824 et 1944"},
  {quoi:"<b>Décès de Fahy 1839</b> — Clotilde Hortense absente"}
 ]},
```

**Compteur :** deux transcriptions de plus. Recompte le total et **harmonise avec le chapeau** (voir §5.2).

**Chapeau, à ajouter :** *Le mariage de Marnay, en 1833, ferme la génération : il nomme la mère de Jeanne ÉCARNOT et date les décès de Noël GRILLOT, de Jean Pierre ÉCARNOT et de Marguerite GARDOT. Les deux mariés étaient orphelins ; sur six ascendants, un seul vivait — **Anne Pierre BERNARDOT, bouchère à Gray**, qui fait le voyage et signe de sa main.*

**Points de vigilance.** Lectures douteuses à conserver entre crochets : **rue de la [Varosse]** et l'heure du décès de Noël, lue [huit] ; **[Glauron]** et **[Drouhard]**, cousins de la mariée en 1833 ; **[Ernest]**, l'adjoint signataire de 1832 ; **[Pierrette] ROUGET**, toujours en attente. Et le prénom de **Joseph GRILLOT le militaire**, porté au 2 décembre 1835 dans l'encart des collatéraux alors que la table décennale de Gray donne un acte au 16 décembre 1835 : **quatorze jours d'écart, ce qui est trop pour une déclaration**. Ou la date de l'encart vient du dossier Léonore et l'acte est tardif, ou les deux ne désignent pas le même enfant. **Signale la divergence dans sa mention** en attendant l'acte de naissance.
