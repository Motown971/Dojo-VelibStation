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
          
#### Lancement du server http et traitement des requêtes HTTP
1. OBJECTIF A : Réussir à lancer un serveur sur http://localhost:8000 (HTTP status = 200) 
    - Test unitaire pour concevoir et vérifier l'implémenttion du fichier **server_0.js** 
        1. Le server est bien lancé
        1. Que le status de la HTTP Response est égal à 200
        - Si mon fichier **server_0.js** se trouve à la racine du projet
        - Si le fichier de serverSpec.js (contenant mes TU) se trouve dans le répertoire spec :
            - Le template du fichier **spec/serverSpec.js** sera le suivant :

            <pre>
            var request = require('request');      
            var server = require('../server_0');

            describe("Lancement d'un server et status response 200 OK", function() {     
                it("Start Server on http://localhost:8000 and error = false", function() {       
  
                });    
            
                it("http://localhost:8000/ returns response.statusCode = 200", function() {
  
                });
            });
            </pre>
          
        - Utilisation du module **request** : 
                - Faire <code>npm install --save-dev request</code>
                - La documentation se trouve sur le site https://www.npmjs.com/package/request
                - Utilisation de la méthode request.get() pour faire un appel vers une URL
        
        - Utilisation Jasmine (cf. http://jasmine.github.io/2.4/introduction.html) :
        <pre>
        expect(....).not.toBe(....)
        expect(....).toEqual(....)
        </pre>
<br />
1. OBJECTIF B : Réussir à router un appel http://localhost:8000/velib vers le fichier './public/index.html'
    - Test unitaire pour concevoir et vérifier l'implémenttion du fichier **server_0.js** 
        1. Le server est bien lancé et la requete http://localhost:8000/velib renvoie un status 200
        1. Vérification que le contenu du tag **&lt;title&gt;** est bien celui du fichier public/index.html
        
        - On rajoutera les lignes ci-dessous dans le fichier **spec/serverSpec.js** :
        
            <pre>
            describe("Lancement d'un server et routage /velib", function() {     
                it("Start Server on http://localhost:8000/velib and error = false", function() {       
  
                });    
            
                it("http://localhost:8000/velib body object &lt;title&gt; = ...", function() {
  
                });
            });
            </pre>
              
        - Pour rappel, la signature de la méthode permettant de créer un server (dans le fichier **server_0.js**) :
        
            <pre>        
            http.createServer(function (request, response) {
            
                // Analyse du contenu de l'object **request** (récupération de l'url d'appel provenant du navigateur web)
            
            }).listen(8000);
            </pre>
        - cf. https://nodejs.org/api/http.html#http_message_url
        <br />
        - Côté serveur, il est nécessaire de pouvoir lire et récupérer le contenu d'un fichier ('./public/index.html')
            - Utilisation du module **fs** (File System cf. https://nodejs.org/api/fs.html#fs_file_system)
            - Le début du fichier **server_0.js** deviendra donc :
                    
            <pre>
            var http = require('http');
            var fs = require('fs');

            http.createServer(function (request, response) {
            
                // Analyse du contenu de l'object **request** (récupération de l'url d'appel provenant du navigateur web)
                
                // Lecture et récupération du contenu du fichier cible avec la méthode fs.readFile()
                // cf. https://nodejs.org/api/fs.html#fs_fs_readfile_file_options_callback
                        
            }).listen(8000);     
            </pre>
            
            - Une fois récupéré, le contenu du fichier cible doit être envoyé vers le navigateur web, avec la méthode **response.end()**
            Voir l'exemple : https://nodejs.org/en/about/
            <br />
        - Test Unitaire : Vérification que le contenu du tag **&lt;title&gt;** est bien celui du fichier public/index.html
            Il existe un module permettant d'utiliser les fonctions jQuery, permettant entre autre de parser le contenu d'une page html.
            Ce module est **cheerio** 
            - Utilisation du module **cheerio** : 
                - Faire <code>npm install --save-dev cheerio</code>
                    - La documentation se trouve sur le site https://www.npmjs.com/package/cheerio
                    - Le début du fichier **server_0.js** deviendra donc :
                    
                    <pre>
                    var request = require('request');
                    var server = require('../server_0');
                    var cheerio = require('cheerio');
                    </pre>
                    - Utilisation de l'instruction **$ = cheerio.load(body);** afin de récupérer un objet JQuery de la chaine de caractère **body**
                            - Avec l'objet **$** il sera possible d'utiliser les méthodes jQuery pour parser des tags html
                    
                    - Utilisation Jasmine (cf. http://jasmine.github.io/2.4/introduction.html) :

                    <pre>
                    expect(....).not.toBe(....)
                    expect(....).toEqual(....)
                    </pre>
