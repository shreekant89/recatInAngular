# recatInAngular

1.	Create a new Angular project using the Angular CLI:
arduinoCopy code
ng new my-angular-app 
2.	Install the react and react-dom packages as dependencies:
Copy code
npm install react react-dom 
3.	Create a new React app inside the Angular project directory:
perlCopy code
cd my-angular-app npx create-react-app my-react-app 
4.	Configure the React app to use a custom publicUrl that matches the Angular app's base URL. Open the my-react-app/package.json file and add the following line:
jsonCopy code
"homepage": "/my-angular-app/" 
5.	In the Angular app, add a new component that will render the React app. For example, create a file src/app/react-wrapper.component.ts with the following contents:
typescriptCopy code
import { Component } from '@angular/core'; @Component({ selector: 'app-react-wrapper', template: ` <div id="react-root"></div> `, }) export class ReactWrapperComponent { ngAfterViewInit() { import('./my-react-app/build/index.js').then(() => { (window as any).ReactDOM.render( (window as any).React.createElement((window as any).App), document.getElementById('react-root') ); }); } } 
This component will load the React app's build file (my-react-app/build/index.js) and render it inside the div with ID react-root.
6.	In the Angular app's main module (src/app/app.module.ts), import the ReactWrapperComponent and add it to the declarations and exports arrays:
typescriptCopy code
import { NgModule } from '@angular/core'; import { BrowserModule } from '@angular/platform-browser'; import { AppComponent } from './app.component'; import { ReactWrapperComponent } from './react-wrapper.component'; @NgModule({ declarations: [AppComponent, ReactWrapperComponent], exports: [ReactWrapperComponent], imports: [BrowserModule], providers: [], bootstrap: [AppComponent], }) export class AppModule {} 
7.	In the Angular app's component template (src/app/app.component.html), add the app-react-wrapper tag to render the React app:
htmlCopy code
<app-react-wrapper></app-react-wrapper> 
8.	Start the Angular app and the React app. In separate terminal windows, run the following commands:
bashCopy code
cd my-angular-app ng serve 
bashCopy code
cd my-angular-app/my-react-app npm start 
Now you should be able to access the Angular app at http://localhost:4200/my-angular-app and the React app at http://localhost:3000. The React app will be embedded inside the Angular app's div with ID react-root.

