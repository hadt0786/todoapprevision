# Todoapp

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 6.1.5.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).


Step    Comment                     command
 1  :   create a Angular app        ng new todo
 
 
 2  :   Connect to Firebase
        
        1- open console.firebase.google.com
        
        2- got to Database(left corner)
            + name  - todoapp
            + accept
        
        3- create a new realtime database
            + Click - Get Started
            + Rules (upper tab)
                    * update - ".read" : true,
                               ".write":true
                    * click Publish

        4- Link tyour firebase app with your application in your virtual studio code
            + In your firebase app -- website-- project
                    * Click on Project Overview
                    * Click </> --> Add FireBase to your app
                    * Copy the configuration 
                                { to }
                    
                    * Back to VS code Editor
                        +open src/environments/enviroments.ts
                            * Add a new property
                                    firebase : {

                                    }
        5- Install Firebase packages
            + under the todoapp --> cd todoapp
            + use this command 
                * npm install firebase angularfire2 --save
                *succesfully imstalled

3   :    Inside your application
        1- go to todo/src/app/app.module.ts
            * add these 2 packages
                **Read the document carefully**
                + import { AngularFireMode } from 'angularfire2';
                + improt { AngularFireDatabaseModule } from 'angularfire2/database';

        2- we need src/app/environments firebase 
            + src/app/app/module.ts
                ++ import { environements } from '../environments/environment';

                ++ src/app/app/module.ts
                    import : [
                        BrowserModule,
                        AngularFireMode.initializeApp(environment.firebase),
                        AngularFireDatabaseModule
                    ]

***** FIREBASE IS SUCCESFFFULY connected to your app *****

***** Design this app using Bootastrap and Font Awesome *****************


4 :      + open src/index.html
                ** Add Bootstrap cdn and Font Awesome 
                  <head>
                  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0=beta.2/css/bootstrap.min.css"/>
                  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css"/>
                  </head>

5 :     Create a Component                  ng g c todo
            + create a folder name todo

6 :     Create a Service
            + Add a new folder under src/app/todo/shared
            + ng g s todo/shared/ todo
            
            ** notice in your app.module.ts **
                + TodoCOmponent is automatically added to your  import
                    and declaration
                
                Summarised structure till now

                *src
                |---*app
                |---|---*todo
                |   |---|----todo.component.ts|html|css
                |   |   |
                |   |   |----*shared --> service
                |   |   |    |------todo.service.ts
                |   |
                |   |----app.module.ts (configured firebase connection)
                |
                |
                |---*environments
                |   |--environment.ts (saved firebase connection detail)
                |
                |
                |---index.html (cdn path for bootstrap and fontawesome)

7 :     Complete Service class

            + src / app / todo / shared / todo.service.ts
                ++  Inject firebase class
                        ** Add import { AngularFireDatabase, AngularFireList} from 'angularfire2/database'

                        ** inside 
                        
                        1- constructor(private firebase : AngularFireDatabase)

                        2- toDoList : AngularFireList<any>
                            constructor(private firebasedb : ANgularFireDatabase)

                        3- to retrieve all data from databse to into this application

                             // Get the item of list from the firebase on the cloud   
                            ** getToDoList(){
                                this.toDoLosy = this.firebasedb.list('titles');
                                return this.toDoList;

                            }

                            // Add item to the firebase on the cloud

                            ** addTitle(title:string){
                                this.toDoList.push({
                                    title:title,
                                    isChecked:false
                                });
                            }

                            // $ --> unique key
                            **  checkOruncheckTitle($key:string, flag:boolean){
                                this.toDoList.update($key, {isChecked:flag});
                            }

                            **removetitle($key : string){
                                this,toDoList.remove($key);
                            }

************** APPLICATION DESIGN STARTS ***********************************

8 :                    + Go to app.component.html
  
                            1- delete the default angular content of an html page

                            2- (short hand) + tab
                                1- div.container
                                    inside -- div.row
                                        inside div.col-md-6.offset-md-3

                            <div class="container">
                            <div class="row">
                            <div class"col-md-6 offset-md-3">
                            !! copy the todo.component.ts
                            !! selector tag 'app-todo'
                            !! And paste here

                             <app-todo></app-todo>   
                            
                            </div>
                            </div>
                            
                            </div>           

***** Design To DO Componet *******

objective -- to list all the list in firebase item from cloud in this component


                                    





















































