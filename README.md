# Genie_Logicielle
Rapport sur le projet json


	
# QUALITE LOGICIELLE  DU PROJET GSON 

	Par: 
    * AGBA Pascal Sébastien
    * KOURIAT Mouhamed.
# Introduction 

*** Pour étudier le projet Gson, afin de faire un rapport sur la qualité ainsi que la conception de ce dernier, on s’est basé sur plusieurs métriques qu’on a vu en cours de GL, et aussi on a effectué des recherches sur internet pour approfondir ses dernières. Ensuite, le calcul des métriques a été fait grâce au programme Sonarqube  déployé grace à docker, qui donne une analyse globale du projet. On a aussi utilisé les plugins suivants sur Intellij :***
    • Sonarlint
    • CodeMR
    • Statistiques
    • MetricsReloaded
    • Jacoco 


## PARTIE 1 

			I-Présentation du projet
			1.1 Utilité du projet  

Le projet est une librairie java qui sert à transformer un objet java en une représentation au format JSON, ou bien à partir d’un fichier ou données JSON, faire une conversion en objet java. Parmi ses fonctionnalités citées dans le readme, cette librairie permet de transformer n’import quel objet java en JSON sans même avoir accès au code source de ce dernier.
 
Le projet est une librairie qu’on peut utiliser pour afin de convertir  des données JSON en objets Java et réciproquement.
L’utilité de ce projet réside dans  son importer dans d’autres projets où le besoin se fera senti. 
Il est aussi précisé dans le README  que pour toute fin utile  , ce projet peut être ajouter dans les dépendances maven.
 
Ce projet utilise un objet JSON , JAVA OBJECT  pour  produire en sortie l’inverse.  La visualisation de  resultat peur se faire au moyen d’un simple print . Le format .json peut egalement être consulter.


##			1.2 Description du projet

Le projet contient un readme pertinent qui commence par donner une définition de ce que fait le projet , ses buts , les méthodes de téléchargement du projet (soit par Gradle ou Ajouter la dépendance en Maven ) . Après il donne une javadoc de toutes les classes du projet , un guide utilisateur et il précise les modifications ajoutées à chaque version du projet ( Change log) . Comme il donne un document qui montre les problèmes rencontrés lors de la conception du projet , et un tutoriel qui explique en détail les classes pour bien comprendre leur utilisation .Ce projet est à jour puisque les dernières modification sont de Mars 2022. Toutefois, il convient de dire que les plus grandes évolutions ont eu lieu en Janvier 2011. Et ce projet à vu le jour en Decembre 2008.  .


En regardant dans le README , on a une section documentation ou on retrouve plusieurs liens, notamment un user guide qui explique de manière générale et précise l’utilisation de cette API. On a aussi une section avec des tutoriels qui proviennent de parties tiers.
Les informations concernant , l’installation ( l’importation ) , l’utilisation sont assez bien expliqués avec des exemples dans le user guide et les vidéos via les parties tiers.
La combinaison de  parties tiers et de dévelloppeurs principaux du projet démontre sa nature de open source projet.  


# 2 Historique du git

## 2.1 Analyse du git


Ce projet à vu le jour le Décembre 2008 et les dernièeres modifications   observées  sont en date de 7 Mars 2022. 


L’évolution du dévelloppement du projet n’a pa suivi une progression linéaire.  En effet,  le graphe montre qu’ au début : il y avait un nombre conséquent de commits   puis une croissance exponentielle en Janvier 2011 suivi par une regression le années suivantes. Objectif atteint ou pas, on ne saurait juger.
 Il   composé  de 112 contributeurs dont 99 principaux ,  et le travail n’a pas été faite de  façon équilibrée. La quasi-totalité du travail a été effectuée par une seule personne  ( 624 commits ) . 
Il y a 26 branches définies et 15 utilisées .
Ce projet a été utilisé à hauteur de 340793 fois
 
Le mécanisme du pull request est utilisé (154 pull request) , et il n’y a pas de pull request en attente .


3 Architecture logicielle
3.1 Utilisation de bibliothèque extérieures

Il y a 7 bibliothèques extérieures référencées :
java.io, java.lang.reflect, java.lang.annotation, java.math, java.text, java.util, java.sql.

Toutes les dépendances sont utiles vu que toutes les classes importées des bibliothèques extérieures sont utilisées .


3.2 Organisation en paquetages

Le projet est organisé en 8 paquetages :

com/google/gson	→ annotation
|	
→ internal → bind → util
|
→ reflect
				|
				→ reflect 
				|
				→ stream

Les paquetages sont effectivement organisés en couches , le paquetage util dépend de bind , bind et reflect dépendent de internal, et annotation , internal , reflect et stream dépendent de com/google/gson . Il existe un cycle entre com/google/gson et internal , entre com/google/gsonet internal/reflect , entre stream et internal.bind .

Il y a 4 niveaux de paquetages : com/google/gson → internal → bind → util . La hiérarchie de paquetages pour les tests suit bien la hiérarchie de paquetages des sources .Il n’existe pas des paquetages qui ne contiennent qu’un seul paquetage sans aucune classe .

Les noms des paquetages ne nous indiquent pas qu’il existe un lien vers une base de données , ni sur les design pattern utilisés.






## 3.3 Répartition des classes dans les paquetages

Il existe 92 classes au total . minimum = 1 , maximum = 26

Toutes les classes ou presque sont-elles dans le même paquetage ? : Non est-ce que des paquetages non feuilles contiennent des classes ? : Oui
Il y a un couplage fort entre le paquetage com.google.gson et les paquetages com.google.gson.internal,com.google.gson.internal.bind.Paquetage com.google.gson est cohésif parce qu’on remarque que dans la classe com.google.gson.GsonBuilder on utilise plusieurs attributs de la classecom.google.gson.Gson.

3.4 Organisations des classes 

La hiérarchie des classes est plutôt plate. D’après les résultats de codemr, il y a 69 classes dont leur arbre d’héritage n’est pas profond (DIT) , et 62 classes qui n’ont pas beaucoup de fils (NOC).

D’après les résultats des analyses des métriques sur le projet , il y a 60 classes avec un couplage faible soit 81.5 % des classes . D’où on peut déduire que les classes du projet sont stables .

D’après les résultats du calcul des métriques sur le paquetage com.google.gson on constate que 52,9% des classes ont un ‘low lack of cohesion’ et 29,3% ont un ‘low-medium lack of cohesion’ , tandis les classes Gson et GsonBuilder sont peu cohésives ,ce qui nous mène à dire que le paquetage est cohésif .


	4 Analyse approfondie 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

		4.1 Tests  

Nombre de tests : 1062 méthodes de tests ,102 classes de tests avec une couverture de tests de 84.7% de code couvert par les tests. Cette métrique nous indique que le code est généralement bien testé, cependant on peut rajouter plus de tests pour avoir une couverture optimale qui se rapproche du 100%. C’est ce qu’on va essayer de mettre en œuvre dans la deuxième partie du projet.
On retrouve des tests unitaires avec des assertions, ainsi que des tests fonctionnels. Pour les tests unitaire une modification sur le code est à prévoir pour changer les fonctions assert ( car détection de code smells sur cette méthode ). Par ailleurs, sur la totalité des tests, deux tests seulement échouent sont testMakeAccessibleWithUnsafe et testDateFormatString ( tests a revoir pour la seconde partie) ce qui donne un pourcentage de succès sur les tests de 98.1%. 

4.2 Commentaires 

Nombre de lignes de commentaires : 3141 soit 27.8% de la totalité des lignes de code ( ligne totale 14940 ). 
On retrouve sur l’ensemble du projet tout type de commentaire : javadoc, licence, code commenté et commentaire pertinent. En moyenne la javadoc couvre 15,76% des classes et 49,85% des méthodes avec un total de 2216 JLOC. On retrouve aussi des classes commentées mais on a nullement une indication pourquoi ces dernières sont sous commentaires. Pour finir 3645 de code non commenté.

4.3 Dépréciation 

Bout de code déprécié : dans la classe JsonElement.java la méthode getAsCharactere() est utilisée alors que cette méthode est dépréciée. Cette méthode est utilisée dans deux classes : JsonArray et JsonPrimitive. JsonArrayest utilisée dans le projet 104 fois et JsonPrimitive est utilisée dans le projet 280 fois. D’après l’IDE, le nom de cette méthode est trompeur, car elle ne prend pas l’élément qui l'appelle comme un caractère mais plutôt comme le premier élément de la chaîne du caractère.


4.4 Duplication de code

 Dans ce projet, il y a :
    • 1000 lignes de code dupliquées  ,
    • 3 Blocs dupliqués : 20 , 
    • fichiers dupliqués : 3 
    • avec une densité de duplication de 2,4%.
      Par ailleurs, nous tenons à signaler que ces duplications proviennent de certaines variables qui sont répétées plusieurs fois, des blocs de code sont dupliqués sur dans LinkedTreeMap et LinkedHashTreeMap.Ces duplications peuvent être supprimées en appliquant les techniques de refactoring pour éliminer les bouts de codes redondants, et initialiser des variables pour éviter de les affecter à plusieurs reprises dans le code notamment dans les classes tests.

4.5 God Classe 

Nombre de méthodes par classes : min = 0 ,max = 53.
Nombre de variables d'instances : Totale de 3916, min = 0, max = 344.
Nombre de lignes de code par classe : Totale de 8078 ( pour le code JAVA ) et 11040 incluant les autres types de fichier ( js, xml..) avec :
min = 0 , max = 1071, avg = 143,88
Pour les grosses classes on se base sur les metrics ATFD, WMC et TCC :
Après avoir analysé les différentes classes du projet, on a pu donner un seuil pour ces 3 metrics , FEW = 2, VERY HIGH = 45 et ONE THIRD = 0.33. Cependant, sur le WMC on a 10 classes qui sont >= VERY HIGH, parcontre pour le ATFD on a pas de classe qui est > FEW, on a juste la classe Gson.java avec un ATFD = 2.
Sur l’ensemble des packages, les classes présentes ne réunissent pas les conditions nécessaires pour être décrites comme GOD CLASS, mais on peut la définir avec un manque de cohésion de classe, une grande complexité cyclomatique et une forte dépendance aux autres classes ( couplage efferent ).
 Ainsi pour LCOM on a JsonElement, $Gson$Types, Gson avec respectivement les valeurs 17, 8 et 7. Pour la complexité cyclomatique on a $Gson$Types, Gson, LinkedHashTreeMap, LinkedTreeMap et TypeAdapters avec les valeurs suivantes :126,89,156,126,181. 

Enfin, le couplage afférent est présent fortement avec plusieurs packages comme google.gson et google.gson.internal.bind. Pour finir, après analyse de ces données la classe qui remplit les 3 conditions sur les métriques mentionnées précédemment, on déduit que la God Classe est Gson.

Pour réduire la complexité cyclomatique  et respecter le principe de responsabilité unique , on peut diviser cette god class en plusieurs classes et donner la délégation de certaines de ses méthodes à d'autres classes.
 Celà permettra de mettre en place des test unitaires à chaque classe et faciliter la maintenance du code.


4.6 Analyses des méthodes 

Complexité cyclomatique : min = 1 , max = 40 , avg = 2,82, médian = 10
La méthode avec la plus grande complexité cyclomatique est JsonReader.doPeak() , en effet cette méthode a 113 lignes de code et 6 lignes de commentaires. On peut en déduire que pour une grosse méthode comme ça, le nombre de commentaires doit être supérieur pour bien détailler le fonctionnement de cette dernière.
 
Nombre de lignes de code de méthodes : min = 1, max = 146, avg = 13,33

On retrouve dans le projet une méthode dans la classe ReflectiveTypeAdapterFactory , la méthode BoundField avec 6 arguments.

Pour les méthodes qui retournent un code d'erreur, on en retrouve dans le projet et elles sont identifiables grâce au mots clés throw new Exception ou bien avec @Exception.


5 Nettoyage de code et code smells 
5.1 Règle de nommage 

Plusieurs  variables du même nom. A tire d’exemple  on a une variable : factories qui est déclarée deux fois. Une mauvaise utilisation d’une variable pourrait causer un bugs susceptibles de se propager dans le reste du programme. 
Pour question de maintenance et de lissibilités , il est nécessaire de modifier le nom d’une des deux pour que les développeurs puissent se repérer si on modifie un bout du code après.
 Aussi on des classes avec un caractère spéciale comme $Gson$Precondition et $Gson$Types, elles ne respectent pas l’expression régulière pour le nom de classe : `^[A-Z][a-zA-Z0-9]*$`.
La classe ISO8601Utils du package (com.google.gson.internal.bind.util) est difficilement prononçable .
De plus private static final Pattern TYPE_PATTERN = Pattern.compile("(?:[\\w$]+\\.)*([\\w$]+)") doit être modifier afin d’éviter les dépasement de la pile. Nous essayerons de rémedier à ça dans la deuxième partie.
Le langage ayant évolué depuis la mise en œuvre de cette API, faire une modification des variables, la syntaxe ainsi que supprimer les mauvaise assignation comme dans le cadre de peeked = PEEKED_END_ARRAY dans la clase String peekedString permettra de faciliter la maintenance pour les  évolutions futures.



5.2 Nombre magique

Pas de nombre magique dans le projet. ( analyse de sonarqube et sonarlint ne donne pas de code smells pour les nombres magiques ).
 		 		

5.3 Structure du code 
 
On a choisi 3 classes dans tous le package stream puis deux dans com/google/gson  et 3 dans les test :,

Parmi cette analyse des classes, on remarque que la structuration du code est mal faite, on retrouve des déclarations de variables d’instance un peu partout dans la classe , un chevauchement des private et publique méthode qui ne respectent pas l’ordre ( public après private ) et aussi la déclaration de classe au sein d’une classe. De plus, sur tout le projet, sonarqube indique l'existence de 12 bugs, parmi les bugs, on retrouve l'appel de certaines méthodes de la classe java.Objet, comme equals sans ajouter le mot clé @Override; ça peut porter confusion à d’autres développeurs, et la solution est soit ajouter Override ou bien renommer carrément les méthodes.
Il y’a aussi les test mal conçu ou des méthodes non couvertes. Dans la suite de notre projet on mettre en place des test, corriger ces erreurs de conception.
 
5.4 Code mort

Le projet Gson est une API, et  c’est normal qu’il existe du code qui ne soit pas appelé en interne.
  On pourrait penser à une suppression de ces code morts mais cela serait une mauvaise pratique  car cette API pourrait être utilisé à d’autres fin  par d’autres développeurs qui éventuellement vont utiliser le code qui n’est pas appelé en interne.
La seule option possible est de mettre à jour ce code en faisant les bons import  et une  adapter la syntaxes afin d’êviter les erreurs syntaxiques signalés dans  Sonarqube.
PARTIE 2
Dans cette partie, nous avons préférés noux concentrés sur l’origine des bugs  puis de les résoudres et au mieux, proposer des solutions pour que les utilisateurs de cette API ne l’utilisent pas avec les bugs.  Ensuite nous  nous concentrons sur une classe pour couvrir les test non effectuer afin d’améliorer la complexité cyclomatique . 
Le travail a donc été fait en deux parties . Une partie en individuel et l’autre en groupe.  Les traces de nos travaux sont donc sur le git.
	6 Amélioration
Partie individuelle
(AGBA Pascal Sébastien)
 **« Dans la classe JsonArray, noud avons la méthode getAsCharacter() qui est identifié comme  code déprécié et que cette dernière . Pour améliorer éviter que cela ne laisse entendre que la qualité du logiciel est moindre, je l’ai donc mis en commentaire. Cet code devrait etre définivement définitivement mais j’ l’ai laissé pour des raisons de traces de travail effectué. Dans  classe $Gson$Types , la méthode static boolean equal (Object a Object b) est sujet de confusion et  entraine un Bug supplémentaire dans l’API. Cette méthode devrait avoir l’annotation @Override ou porter le qualificatif public. C’est ce qui a été fait et le Bug n’y est plus. Toutes les classes ayant besoin besoin de l’annotation @Override  ont été renomées ainsi et cela fait passe les Bugs de 12 à 8.**
 **Sonarqube signale aussi le mauvais nommage des attributs car ces derniers ne diffèrent de la classe dans laquelle ils sont, que par la première lettre (Majuscule ou minuscule).  Renommer ces attributs revient à rédefenir la classe Builder . Ce qui serait fastidieux. Chaque developpeur souhaitant utiliser l’API devra donc faire un héritage et ensuite renommer 	avec des attributs respectant la dernières syntaxe de Java.»**


