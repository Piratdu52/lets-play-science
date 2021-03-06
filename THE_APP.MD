Les specs collectives de l'application hypo-thétique
---------------------------------------------------
*Avant de concevoir une application, c'est une bonne idée de savoir à quoi elle ressemble, d'analyser quels sont les enjeux techniques de sa réalisation*

**Ce document n'est pas du tout déstiné spécifiquement aux développeurs, bien au contraire. On a tous une expérience utilisateur.**

Sommaire
--------------------------------------------------

- I. [Définitions](#I)
    1. [Post](#I.1)
    2. [Commentaire](#I.2)
    3. [Carte Heuristique / Mind map](#I.3)
    4. [Arbre sémantique](#I.4)
    5. [Hash sémantique](#I.5)
    6. [Filtre sémantique](#I.6)
    7. [Fusion](#I.7)
    8. [Soumission](#I.8)
    9. [Version](#I.9)
    10. [Post cible](#I.10)
    11. [Post source](#I.11)
    12. [Référence](#I.12)
    13. [Défi](#I.13)
- II. [Cycle de vie d'un défi](#II)
- III. [Associations sémantiques](#III)
- IV. [Versionnement](#IV)
- V. [Rôles](#V)
- VI. [Sources de données](#VI)

<a name="I"></a>
## I. Définitions & Concepts
*On va p'tet commencer par s'accorder sur le sens des mots nan?*

<a name="I.1"></a>
#### 1. Post
Document collaboratif qui propose une approche de réponse possible.  
**Problème** : comment correctement circoncir le périmètre de la réponse ?

<a name="I.2"></a>
#### 2. Commentaire
Observation, critique, avis fait sur un post. Ce n'est pas un document collaboratif.

<a name="I.3"></a>
#### 3. Carte Heuristique / Mind map
Vue en 2D sous forme de diagramme de graphe ordonné des liens sémantiques *entre posts*

<a name="I.4"></a>
#### 4. Arbre sémantique
*[README.md#II.3.b](README.md#II.3.b)*  
Vue sous forme d'arbre des liens sémantiques *entre posts*  
**Remarque** : Une feuille peut être dupliquée sur différents noeuds !
Ex :
> ├── Ascenceurs spatiaux  
│   ├── Ascenseur  
│   ├── Skyhook  
│   └── …  
├── Propulsion  
│   ├── Capsules à explosions nucléaire  
│   ├── Fusées  
│   │   ├── Explosion  
│   │   ├── Hydrogène  
│   │   └── …  
│   └── …  
└── …

<a name="I.5"></a>
#### 5. Hash sémantique
*[README.md#II.3.c](README.md#II.3.c)*  
Chemin de l'arbre sémantique exprimé sous forme de hashtag, chaque feuille est séparée de son noeud par un `:`

Ex :
> `#Propulsion:Fusées:Explosion`

<a name="I.6"></a>
#### 6. Filtre sémantique
Expression textuelle permettant de filtrer les posts suivant les noeuds sélectionnés
Ex :
> `#Propulsion:Fusées`

Affiche tous les posts référés dans le chemin `Propulsion:Fusées`.  

**Remarque** :  
> `#Fusées`

Va aggréger (fusionner) tous les noeuds appellés `Fusées`

<a name="I.7"></a>
#### 7. Fusion
Action de fusionner deux posts sémantiquement proches.
- Questions : qui propose la fusion ? Un utilisateur peut-il suggérer la fusion de deux posts qu'il trouve proches? P'tet une option "proposer une fusion", cette dernière devant être validée par les deux auteurs...

<a name="I.8"></a>
#### 8. Soumission
*Non, pas le machin de Houellebecq*
Action de soumettre à l'auteur d'un post une nouvelle **version** du document.

<a name="I.9"></a>
#### 9. Version
Une version figée d'un post, qu'on peut rétablir plus tard.
**Remarque** : Une fusion créée automatiquement une nouvelle version du **post cible**.

<a name="I.10"></a>
#### 10. Post cible
C'est la destination (reçu par l'hôte) de la fusion

<a name="I.11"></a>
#### 11. Post source
C'est l'origine (proposé par l'offreur) de la fusion

<a name="I.12"></a>
#### 12. Référence
Référence (source littéraire, culturelle) associée à un post.

<a name="I.13"></a>
#### 13. Défi
Question soumise pour l'organisateur de l'évênement, ici Léo, et par extension, tous le processus d'élaboration de réponses par les participants.

<a name="II"></a>
### II. Cycle de vie d'un défi
*Description détaillée du cycle de vie d'un [défi](#I.13)*

<a name="III"></a>
### III. Associations sémantiques
*Aspects techniques des associations sémantiques*

<a name="IV"></a>
### IV. Versionnement
*Aspects techniques sur le versionnement des posts*

<a name="V"></a>
### V. Rôles
*Déscription détaillée des rôles endossés par les participants*

<a name="VI"></a>
### VI. Sources de données
Les sources de données mentionnées sont les sources techniques constituant l'ensemble des entités présentées [ci-dessus](#I).
Catégorisons de types de données :
 - les données primaires :
  - Post [cf I.1](#I.1)
  - Commentaire [cf I.2](#I.2)
 - les données d'associations sémantiques
  - Tags [cf I.5](#I.5)
  - Structure d'arbre ou de graphe ([cf I.3](#I.3), [I.4](#I.4))
  - ...

#### Solution 1 :
Créer une source de données spécifique et propre, une nouvelle base de donnée. Cela permettrai la mise en oeuvre de certains cas d'utilisation comme la fusion, les gestions des cycles de vies, la gestion des versions, etc...

**pros**
- Permet l'édition colaborative, versionnement et fusion
- Donne globalement plus de marge de manoeuvre à la gestion des contenus par l'application

**cons**
- Séparé de youtube, effort pour le participant

#### Solution 2 :
Utiliser pour les données primaires les commentaires de Youtube et leurs réponses. Cela limitera certain cas d'utilisation, mais cela permettra de ne pas perturber les utilisateurs de Youtube, qui pourront continuer à faire des propositions, faire leurs réponses comme d'habitude ! Les utilisateurs qui voudrons prendre du recul pourrons alors passer sur la présente application pour gérer ces commentaires, les regrouper, les tagger, etc... Les données d'associations sémantiques seraient, quant à elle, stockées spécifiquement. Ce qui est interessant c'est que cette mécanique serait accessible alors pour toutes les chaines Youtube.

On pourrait aussi imaginer une syntaxe pour que l'application "filtre" les messages qui ont un rapport, permettant par exemple une intégration avec les hashs sémantiques!

**pros**
- Pas de changement brutal des habitudes pour les participants
- Ouverture de la plateforme à toutes les chaines youtube
- Authentification par youtube ou google+, c'est un parti pris

**cons**
- Authentification par youtube ou google+, c'est un parti pris
- Versionnement des posts rendu plus compliqué
