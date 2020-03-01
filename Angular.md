## Angular v5

> Make AOT the default
> Type checking in templates
> Remove *.ngfactory.ts files
> Tree-Shakeable components

## Angular v6
```
Typescript 2.7+ supports
ng add @angular/pwa app manifest and service worker
ng add @ng-bootstrap/schematics — Add ng-bootstrap 
ng add @angular/material — Install and setup Angular Material
ng add @angular/elements — Add the needed document-register-element.js polyfill and dependencies for Angular Elements
angular.json
creating and building libraries ng generate library <name>
services referencing modules
```
```javascript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class MyService {
  constructor() { }
}
```
> updated to use v6 of RxJS rxjs-compat

## Project structure
```
src/                         project source code
|- app/                      app components
|  |- config/                config (configuration files)
|  |- core/                  core module (singleton services and single-use components)
|  |- shared/                shared module  (common components, directives and pipes)
|  |- app.component.*        app root component (shell)
|  |- app.module.ts          app root module definition
|  |- app-routing.module.ts  app routes
```

## Angular Module Configuration Properties


#### imports
```
This property is used to specify the Angular modules that the application requires. The **BrowserModule, FormsModule, and HttpModule** modules provide core Angular functionality. The ModelModule is the custom feature module that contains the data model for the example application.
```

#### providers 
```
This property is used to specify services for the dependency injection feature. This property is empty in the root module because the only service currently in the Angular application is defined in the model feature module.
```

#### declarations 
```
This property is used to provide Angular with a list of the **building blocks** used in the application. For the **root module**, this property specifies AppComponent, which is the only building block in the application at the moment.
```

#### bootstrap 
```
This property specifies the **root component for the application**, which will be used to start the application. For the example application, this property is set to AppComponent, which is the only component in the Angular application currently.
```

**app.module.ts**
```javascript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';
import { AppComponent } from './app.component';
import { ModelModule } from "./models/model.module";
@NgModule({
 declarations: [AppComponent],
 **imports: [BrowserModule, FormsModule, HttpModule, ModelModule],**
 providers: [],
 bootstrap: [AppComponent]
})
export class AppModule { }
```

## Component Configuration

>  Repository Class in the app.component.ts 
```javascript
import { Component } from '@angular/core';
import { Repository } from "./models/repository";
import { Product } from "./models/product.model";
@Component({
 selector: 'app-root',
 templateUrl: './app.component.html',
 styleUrls: ['./app.component.css']
})
export class AppComponent {
 constructor(private repo: Repository) { }
 get product(): Product {
    return this.repo.product;
 }
}
```

#### Selector 

This property is used to specify the HTML element that the component will be responsible for managing. For this component, the selector property tells Angular that the component will manage the app-root element

#### TemplateUrl

This property is used to specify the **component’s template**, which is the **HTML content that will be displayed to the user**

#### StyleUrls

This property is used to specify one or more CSS stylesheets that will be applied to the component’s template content. **Bootstrap CSS**


## app-root
```
The HTML document received by the browser contains the app-root element into which the dynamic content produced by the Angular application is inserted, and it also contains the script elements for JavaScript files that contain the Angular framework and the custom application and data
model classes. 
```

## Angular Lifecycle Methods

```
ngOnChanges             : called when an input or output binding value changes
ngOnInit                : after the first ngOnChanges
ngDoCheck               : developer’s custom change detection
ngAfterContentInit      : after component content initialized
ngAfterContentChecked   : after every check of component content
ngAfterViewInit         : after component’s view(s) are initialized
ngAfterViewChecked      : after every check of a component’s view(s)
ngOnDestroy             : just before the directive is destroyed.

```

## Lifecycle Hooks Methods

```
ngOnChanges()           : Responds when Angular (re)sets data-bound input properties. The method receives a SimpleChanges object of current and previous 
                          property values. Called  before ngOnInit(), and whenever one or more data-bound input properties changes.
ngOnInit()              : Initializes the directive/Component after Angular first displays the data-bound properties and sets the directive/Component's input properties.
                          Called once, after the first ngOnChanges() method.
ngDoCheck()             : Detects and acts upon changes that Angular can't, or won't, detect on its own. Called during every change detection run, 
                          immediately after ngOnChanges() and ngOnInit().
ngAfterContentInit()    : Responds after Angular projects external content into the Component's view/the view that a directive is in. Called once after the first 
                          ngDoCheck() method.
ngAfterContentChecked() : Responds after Angular checks the content projected into the directive/Component. Called after the ngAfterContentInit() method and every 
                          subsequent ngDoCheck() method.
ngAfterViewInit()       : Responds after Angular initializes the Component's views and child views/the view that a directive is in. Called once after the 
                          first ngAfterContentChecked() method.
ngAfterViewChecked()    : Responds after Angular checks the Component's views and child views/the view that a directive is in. Called after the ngAfterViewInit() method
                           and every subsequent ngAfterContentChecked() method.
ngOnDestroy()           : Cleans up just before Angular destroys the directive/Component. Unsubscribes Observables and detaches the event.Handlers to avoid 
                          memory leaks: Called just before Angular destroys the directive/Component.
```

## Form Features

```
Form validation
Custom validators
Nested forms
Dynamic forms
Template-driven forms
```

## State of form

```
{{myform.form.touched}}
{{myform.form.untouched}}
{{myform.form.pristine}}
{{myform.form.dirty}}
{{myform.form.valid}}
{{myform.form.invalid}}
```

## The Built-in Angular Piples

#### Number 
>This pipe is used for specify the number of integer and fraction digits shown for a number value.
```javascript

```

#### Currency 
>This pipe is used to format a number value as a currency amount.
```javascript
{{product.price | currency:"USD":true }}
```

#### Percent
>This pipe is used to format a number value as a percentage.
```javascript

```

#### Uppercase 
>This pipe is used to convert a string value to uppercase characters.
```javascript
{{ name | UppercasePipe }} 
```

#### lowercase 
>This pipe is used to convert a string value to lowercase characters.
```javascript

```

#### json
>This pipe is used to serialize an object to JSON data.
```javascript
{{employees | json }}
```

#### slice 
>This pipe is used to select elements from an array.
```javascript

```

#### Date
>This pipe is used to select elements from an Date.
```javascript
{{ birthday | date:"MM/dd/yy" }}
```

## Data binding


## Base Service with Promise
```javascript
import { Http, Headers } from '@angular/http';
import { Inject, Injectable } from '@angular/core';
import 'rxjs/add/operator/map';

@Injectable()
export abstract class BaseService {
  config: String;
  http:   Http;
  modelName: string;
  model: any;

  constructor(@Inject(Http) http: Http) {
    this.http   = http;
    this.config = 'http://yourBackend.url'
  }

  mapListToModelList (list: Array<Object>) {
    list.forEach((item, index) => {
      list[index] = this.mapModel(item);
    });
    return list;
  }

  mapModel(model: any) {
    return this.model(model);
  }

  findById(id: number, populate: Array<string> = null) {
    return new Promise((resolve, reject) => {
      let url = this.config + '/' + this.modelName + '/' + id;
      if (populate) {
        url = url + '?populate=' + populate.join(', ');
      }
      console.log('URL', url);
      this.http.get(url)
        .map(res => res.json())
        .subscribe(res => {
          if (res.error) {
            reject(res.error);
          } else {
            resolve(this.mapModel(res));
          }
        });
    });
  }

  find(populate: Array<string> = null) {
    return new Promise((resolve, reject) => {
      let url = this.config + '/' + this.modelName;

      if (populate) {
        url = url + '?populate=' + populate.join(', ');
      }

      this.http.get(url)
        .map(res => res.json())
        .subscribe(res => {
          if (res.error) {
            reject(res.error);
          } else {
            resolve(this.mapListToModelList(res));
          }
        });
    });
  }

  upsert(model: any) {
    return new Promise((resolve, reject) => {
      let url = this.config + '/api/' + this.modelName;

      var headers = new Headers();
      headers.append('Content-Type', 'application/json');
      headers.append('Accept', 'application/json');

      this.http.put(url, JSON.stringify(model), {headers : headers})
        .map(res => res.json())
        .subscribe(res => {
          console.log(res);
          if (res.error) {
            reject(res.error);
          } else {
            resolve(this.mapModel(res));
          }
        });
    });
  }

  create(model: any) {
    return new Promise((resolve, reject) => {
      let url = this.config + '/' + this.modelName;

      var headers = new Headers();
      headers.append('Content-Type', 'application/json');
      headers.append('Accept', 'application/json');

      this.http.post(url, JSON.stringify(model), {headers : headers})
        .map(res => res.json())
        .subscribe(res => {
          console.log(res);
          if (res.error) {
            reject(res.error);
          } else {
            resolve(this.mapModel(res));
          }
        });
    });
  }
}
```

