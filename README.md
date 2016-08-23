# Dojo-VelibStation
Nous voulons consulter les stations Velib existantes à Paris

####  Prerequisites
1.  Création d'un répertoire de travail
par exemple : C:\work\dojo\angularJS\exo1

1. Initialiser un projet node
Il faut se placer dans le répertoire nouvellement créé, puis executer la commande
```javascript
npm init
```

1. Installation des outils et plugins npm
    1. Il faut installer le framework Karma et et l'outil de test Jasmine
    ```
    npm install karma --save-dev
    npm install karma-jasmine karma-chrome-launcher --save-dev
    ```
    1. Il faut installer, globalement, le "Karma Commandline Interface", afin de pouvoir faire un Karma start plus facilement
    ```
    npm install -g karma-cli
    ```
    Pour plus d'informations à propos de l'installation de Karma : https://karma-runner.github.io/0.13/intro/installation.html
    
    1. Dans une premier temps, l'un des buts de ce premier dojo, sera de lire des données contenues dans un fichier csv
    Le plugin [csv-load-sync](https://www.npmjs.com/package/csv-load-sync) fait très bien ce travail.
    ```
    npm install csv-load-sync --save-dev
    ```
    
    1. Nous aurons besoin d'ouvrir automatiquement un navigateur, après le lancement du serveur local.
    Le plugin 'open' fait très bien cette action.
    ```
    npm install open --save-dev
    ```
    
1. Installation de Bower et des dépendences utilisées par l'application
```
npm install bower --save-dev
```
    1. Initialisation du fichier bower.json, qui va contenir la liste des dépendences nécessaires à l'application.
    ```            
    bower init
    ```
    1. Installation d'AngularJS
    ```            
    bower install angular --save-dev
    ```
    1. Installation de Bootstrap
    ```            
    bower install bootstrap-css --save-dev
    ```
    1. Installation de JQuery
    ```            
    bower install jquery --save-dev
    ```

1. Si besoin, il est possible de lancer un server javascript
```
node <nom_du_fichier_server>     # par exemple s'il existe un fichier server.js : node server
```

<br />
<hr>

##  Theme de l'exercice
Nous voulons consulter les stations Velib existantes à Paris.

1.  Via le site http://opendata.paris.fr/explore/dataset/stations-velib-disponibilites-en-temps-reel/export/
nous allons récupérer les fichiers *.csv et *.json, contenant la liste des points Vélib.

1.  Avec AngularJS, nous voulons afficher ces données, et pouvoir les manipuler.

###  Utilisation d'un template html et de quelques données
* index_0.html
* stationsVelib.xlsx


<br />
<hr>
##  Best practices
*  Comment découper en sous-répertoires notre application AngularJS ? 
Nous allons suivre les recommandations standards (https://scotch.io/tutorials/angularjs-best-practices-directory-structure)

```
app/
----- shared/   // Composants réutilisables
---------- composantA/
--------------- composantADirective.js
--------------- composantAView.html
---------- composantB/
--------------- composantBDirective.js
--------------- composantBView.html
----- components/   // Chaque composant est traité comme une mini application AngularJS
---------- home/
--------------- homeController.js
--------------- homeService.js
--------------- homeView.html
---------- blog/
--------------- blogController.js
--------------- blogService.js
--------------- blogView.html
----- app.module.js
----- app.routes.js
assets/
----- img/      // Images et icons pour notre application
----- css/      // Tous les fichiers de style CSS, et les fichiers de style lié (SCSS ou LESS)
----- js/       // Simples fichiers JavaScript écrits pour notre application, et qui ne sont pas pour AngularJS
----- libs/     // Libraries externes comme jQuery, Moment, Underscore, etc.
index.html
```

<br />
<hr>
##  Utilisation d'un server nodejs, pour gérer les I/O, dont le controller angularjs a besoin
1. Bonnes pratiques nodejs et angularjs, concernant l'organisation des répertoires, des *.js, etc...
    1. Cf. ci-dessus : Création des répertoires
        * app/components/velib
        * app/server/data
        * app/server/modules
        * public

1. Méthode TDD : Utilisation de Jasmine
    1. Installation
    ```
    npm install -g jasmine
    jasmine init
    ```

    1. Utilisation
        * http://jasmine.github.io/2.4/introduction.html
        * Création d'un fichier de test dans le répertoire **spec** : spec/serverSpec.js
        ```
        describe('La description de ma suite de tests jasmine', function() {
          it('ce qui est vrai doit toujours le rester !', function() {
            expect(true).toBe(true);
          });

          it('un ticket de métro parisien vaut 1,80€', function() {
          	var ticketRatp = getTicketMetro(1);
          	expect(ticketRatp.prix).toEqual(1.80);
          });
        });
        ```

1. Server NodeJS
    - NodeJS fourni plusieurs modules/plugins de base, qui permettent :
        - Lecture/écriture de fichiers
        - Opérations sur les propriétés des fichiers/répertoires
        - Création d'un serveur
        - Gestion des requêtes/réponses d'un serveur

    - Importation d'un module dans un fichier javascript (côté serveur)
      * déjà fourni par NodeJS
      * ou bien installé avec la commande npm install --save-dev
      * ou bien un module créé, et qui ce trouve dans l'arborensce du projet (ex: server/modules/le-nom-de-mon-propre-module)
        * Exemple d'importation du module [http](https://nodejs.org/api/http.html) permettant de créer un serveur HTTP :
          Syntaxe dans le fichier server_0.js

            ```
            var http = require('http');
            ```
          Voir l'exemple : https://nodejs.org/en/about/
