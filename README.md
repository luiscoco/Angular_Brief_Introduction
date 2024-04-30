# Angular: brief introduction

Angular is a popular framework developed by Google for building dynamic web applications

It is based on TypeScript and provides a robust set of tools and components to manage the complexity of modern app development

## Setting Up Angular in Visual Studio Code (VSCode)

To work with Angular in VSCode effectively, you'll want to set up your development environment properly

Here’s a step-by-step guide on how to get started:

**Install Node.js and npm**: Angular requires Node.js and npm (node package manager). You can download and install them from nodejs.org.

**Install Angular CLI**: Angular CLI is a command-line interface tool that you use to initialize, develop, scaffold, and maintain Angular applications. You can install it globally using npm:

```bash
npm install -g @angular/cli
```

Create a New Angular Project: Once Angular CLI is installed, you can create a new Angular project by running:

```bash
ng new my-angular-app
```

This command creates a new folder named my-angular-app with all the necessary Angular files and dependencies

**Open the Project in VSCode**: Open VSCode, then open the project folder you just created by selecting File > Open Folder... and choosing your project directory

**Install Angular Language Service**: To enhance your development experience, install the Angular Language Service extension in VSCode

It provides a rich editing experience for Angular templates, such as autocompletion, error checks, and hints

Useful Extensions for Angular Development in VSCode

**Angular Language Service**: Offers autocompletion, error checking, hints, and navigation inside Angular templates

**Angular Snippets**: Provides TypeScript, HTML, Angular Material, and Ngrx snippets

**Prettier - Code formatter**: Automatically formats TypeScript, CSS, and HTML code according to a set style

**ESLint**: Integrates ESLint JavaScript into VSCode for better code quality and style

## Sample Angular Project Structure

Here’s an example of a basic Angular project structure created by Angular CLI:

```java
my-angular-app/
├── e2e/
├── node_modules/
├── src/
│   ├── app/
│   │   ├── app-routing.module.ts
│   │   ├── app.module.ts
│   │   ├── app.component.css
│   │   ├── app.component.html
│   │   ├── app.component.spec.ts
│   │   └── app.component.ts
│   ├── assets/
│   ├── environments/
│   │   ├── environment.prod.ts
│   │   ├── environment.ts
│   ├── favicon.ico
│   ├── index.html
│   ├── main.ts
│   ├── polyfills.ts
│   ├── styles.css
│   └── test.ts
├── angular.json
├── package.json
├── tsconfig.app.json
├── tsconfig.json
└── tsconfig.spec.json
```

Each file and directory serves a specific purpose:

**app.component.***: Defines your app's root component including its HTML template, CSS styles, and TypeScript class

**app.module.ts**: Declares the root module that tells Angular how to assemble the application

**angular.json**: Contains default settings for build, serve, and deploy tasks

**environments/**: Includes settings for different environments like development and production

This setup provides a strong foundation for developing complex applications with Angular in VSCode

By utilizing these tools and extensions, you can significantly enhance your productivity and code quality

## 1. Angular Components

Components are the building blocks of Angular applications. They control a patch of screen called a view. Here’s an example of a simple Angular component:

```typescript
// app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'My Angular App';
}
```

And the corresponding HTML template:

```html
<!-- app.component.html -->
<h1>Welcome to {{ title }}!</h1>
```

Type the following command to generate a new component

Replace your-component-name with the desired name for your component:

```
ng generate component your-component-name
```

Or, you can use the shorter alias ng g c:

```
ng g c your-component-name
```

This command will create a new directory under the **src/app** folder with the component files, including TypeScript, HTML, CSS, and a spec file for testing

Make sure you have Angular CLI installed globally (**npm install -g @angular/cli**) and that your terminal is opened in the root directory of your Angular project where the angular.json file is located

## 2. Angular Services

Services in Angular are reusable data providers that can be injected into components. Here's an example of a simple logging service:

```typescript
// log.service.ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class LogService {
  log(msg: any) {
    console.log(new Date() + ": " + JSON.stringify(msg));
  }
}
```

This service can be used in any component:

```typescript
// app.component.ts
import { Component } from '@angular/core';
import { LogService } from './log.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  constructor(private logger: LogService) {}

  performAction() {
    this.logger.log('Action performed');
  }
}
```

## 3. Angular Routing

Routing in Angular allows you to navigate between different components. Here's a basic setup for routing:

```typescript
// app-routing.module.ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home.component';
import { AboutComponent } from './about.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

Components used in routing:

```typescript
// home.component.ts
import { Component } from '@angular/core';

@Component({
  template: '<h2>Home Page</h2>'
})
export class HomeComponent {}
```

```typescript
// about.component.ts
import { Component } from '@angular/core';

@Component({
  template: '<h2>About Page</h2>'
})
export class AboutComponent {}
```

## 4. Data Binding

Angular supports different types of data binding, such as **property binding**, **event binding**, and **two-way binding**:

```html
<!-- app.component.html -->
<input [value]="name" (input)="name = $event.target.value">
<p>Your name is: {{ name }}</p>
<button (click)="clickMe()">Click Me</button>
```

```typescript
Copy code
// app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  name: string = '';

  clickMe() {
    alert('Button clicked!');
  }
}
```

In Angular, components can communicate using a variety of methods depending on the relationship between the components (parent to child, child to parent, or unrelated components). Below are examples for each scenario, illustrating effective communication patterns using @Input(), @Output(), services, and Angular’s event-driven architecture.

## 5. Parent to Child Communication

Parent components can pass data to child components using @Input() decorators

**Child Component (Receives data)**:

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<p>Received message: {{ message }}</p>`
})
export class ChildComponent {
  @Input() message: string;
}
```

**Parent Component (Sends data)**:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `<app-child [message]="parentMessage"></app-child>`
})
export class ParentComponent {
  parentMessage = 'Hello from Parent!';
}
```

## 6. Child to Parent Communication

Child components can send data back to the parent using the @Output() decorator and EventEmitter. Here’s how:

**Child Component (Sends data)**:

```typescript
import { Component, EventEmitter, Output } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<button (click)="sendMessage()">Send Message to Parent</button>`
})
export class ChildComponent {
  @Output() messageEvent = new EventEmitter<string>();

  sendMessage() {
    this.messageEvent.emit('Hello from Child!');
  }
}
```

**Parent Component (Receives data)**:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `<app-child (messageEvent)="receiveMessage($event)"></app-child>
             <p>Message received: {{ message }}</p>`
})
export class ParentComponent {
  message: string;

  receiveMessage(message: string) {
    this.message = message;
  }
}
```

## 7. Communication Between Unrelated Components

For components that are not in a direct parent-child relationship, you can use a shared service with observables to facilitate communication:

**Shared Service**:

```typescript
import { Injectable } from '@angular/core';
import { BehaviorSubject } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class MessageService {
  private messageSource = new BehaviorSubject<string>('default message');
  currentMessage = this.messageSource.asObservable();

  changeMessage(message: string) {
    this.messageSource.next(message);
  }
}
```

**Component A (Sends data)**:

```typescript
import { Component } from '@angular/core';
import { MessageService } from './message.service';

@Component({
  selector: 'app-component-a',
  template: `<button (click)="newMessage()">Send New Message</button>`
})
export class ComponentA {
  constructor(private messageService: MessageService) {}

  newMessage() {
    this.messageService.changeMessage('Hello from Component A!');
  }
}
```

**Component B (Receives data)**:

```typescript
import { Component, OnInit } from '@angular/core';
import { MessageService } from './message.service';

@Component({
  selector: 'app-component-b',
  template: `<p>{{ message }}</p>`
})
export class ComponentB implements OnInit {
  message: string;

  constructor(private messageService: MessageService) {}

  ngOnInit() {
    this.messageService.currentMessage.subscribe(message => this.message = message);
  }
}
```

These examples cover the primary methods by which components can communicate in Angular\

By utilizing **@Input()**, **@Output()**, and **services with observables**, Angular provides flexible solutions for component interactions across a variety of scenarios, supporting clean and manageable data flow within applications.

# More advance Angular features

## 1. HTTP Service (HttpClient)

Angular's HttpClient service is used to make HTTP requests to a server. Here's how you might use it to interact with an API:

```typescript
// post.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';
import { Post } from './post.model';  // Assume a model interface is defined

@Injectable({
  providedIn: 'root'
})
export class PostService {

  constructor(private http: HttpClient) { }

  getPosts(): Observable<Post[]> {
    return this.http.get<Post[]>('https://jsonplaceholder.typicode.com/posts');
  }
}
```

## 2. Reactive Forms

Reactive forms provide a model-driven approach to handling form inputs whose values can change over time. This example shows how to set up a reactive form:

```typescript
// app.component.ts
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, Validators } from '@angular/forms';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent implements OnInit {
  myForm: FormGroup;

  ngOnInit() {
    this.myForm = new FormGroup({
      'name': new FormControl(null, Validators.required),
      'email': new FormControl(null, [Validators.required, Validators.email])
    });
  }

  onSubmit() {
    console.log(this.myForm.value);
  }
}
```

The corresponding HTML:

```html
<!-- app.component.html -->
<form [formGroup]="myForm" (ngSubmit)="onSubmit()">
  <input formControlName="name" placeholder="Name">
  <input formControlName="email" placeholder="Email">
  <button type="submit" [disabled]="!myForm.valid">Submit</button>
</form>
```

## 3. Dependency Injection (DI)

Angular’s dependency injection system allows you to inject dependencies in components and services. Here is an example using a service that depends on another service:

```typescript
// logger.service.ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class LoggerService {
  log(message: string) {
    console.log(message);
  }
}
```

```typescript
// user.service.ts
import { Injectable } from '@angular/core';
import { LoggerService } from './logger.service';

@Injectable({
  providedIn: 'root'
})
export class UserService {
  constructor(private logger: LoggerService) {}

  createUser(name: string) {
    this.logger.log(`User ${name} created`);
    // additional logic to create a user
  }
}
```

## 4. RxJS Observables

RxJS Observables are a powerful feature used extensively in Angular for managing asynchronous operations. Here’s how you might use observables in a service with a component:

```typescript
// timer.service.ts
import { Injectable } from '@angular/core';
import { Observable, timer } from 'rxjs';
import { map } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class TimerService {
  getTimer(): Observable<string> {
    return timer(0, 1000).pipe(
      map((tick) => new Date().toLocaleTimeString())
    );
  }
}
```

```typescript
// app.component.ts
import { Component, OnDestroy } from '@angular/core';
import { Subscription } from 'rxjs';
import { TimerService } from './timer.service';

@Component({
  selector: 'app-root',
  template: `<p>Current time: {{ currentTime }}</p>`
})
export class AppComponent implements OnDestroy {
  currentTime: string;
  private timerSubscription: Subscription;

  constructor(private timerService: TimerService) {
    this.timerSubscription = this.timerService.getTimer().subscribe(time => {
      this.currentTime = time;
    });
  }

  ngOnDestroy() {
    this.timerSubscription.unsubscribe();
  }
}
```

## 5. Angular Directives

### 5.1. ng-content 

**ng-content** directive is used for content projection

This allows you to create components that can accept dynamic HTML content from the parent component

It's like creating a placeholder in a component template that can be filled with custom content defined outside of the component.

Example:

**ParentComponent.html**

```html
<app-child>
  <p>This content is projected from the ParentComponent into the ChildComponent.</p>
</app-child>
```

**ChildComponent.html**

```html
<div>
  Here is some content inside the ChildComponent.
  <ng-content></ng-content> <!-- Place where projected content will appear -->
</div>
```

Here, the ```<p>`` tag in the ParentComponent's template will appear inside the ng-content tag in the ChildComponent.

### 5.2. ng-template

**ng-template** directive is a template element used in Angular to render HTML views dynamically

The content inside ng-template is not rendered directly; instead, it can be used as a template or blueprint to be instantiated programmatically by Angular based on certain conditions or contexts

Example:

```html
<ng-template #loadingTemplate>
  <div>Loading...</div>
</ng-template>

<div *ngIf="isLoading; else loadingTemplate">
  Content is loaded.
</div>
```

In this example, if isLoading is true, "Content is loaded." will be displayed

If isLoading is false, the content inside ng-template tagged with loadingTemplate will be displayed, which is "Loading..."

### 5.3. ng-container

**ng-container** directive is a grouping element that doesn't interfere with styles or layout because Angular doesn't put it into the DOM

It's useful for conditional grouping of elements without adding extra elements to the DOM

Example:

```html
<div>
  <ng-container *ngIf="isVisible">
    <p>This paragraph is only added to the DOM if 'isVisible' is true.</p>
    <p>This is another paragraph that also depends on 'isVisible'.</p>
  </ng-container>
</div>
```

In this case, both paragraphs are only rendered if isVisible is true

**ng-container** is especially useful when you want to use structural directives like **ngIf**, **ngFor**, or **ngSwitch** on multiple elements simultaneously without wrapping them in an actual DOM element like a div

### 5.4. *ngIf

*ngIf is a structural directive used to add or remove an element from the DOM based on a given condition. This is useful for conditional display of content

Example:

```html
<p *ngIf="user.isLoggedIn">Welcome back, {{ user.name }}!</p>
```

This paragraph will only be rendered if user.isLoggedIn is true

### 5.5. *ngFor

*ngFor is another structural directive used for rendering a list of items. It repeats the host element for each element in an array

Example:

```html
<ul>
  <li *ngFor="let item of items">{{ item }}</li>
</ul>
```

This code will render an unordered list (```<ul>```), with each item in the items array appearing as a list item (```<li>```)

### 5.6. *ngSwitch, *ngSwitchCase, and *ngSwitchDefault

These directives are used together to display content conditionally, much like switch statements in many programming languages.

Example:

```html
<div [ngSwitch]="user.role">
  <p *ngSwitchCase="'admin'">You have admin access.</p>
  <p *ngSwitchCase="'user'">You are a logged-in user.</p>
  <p *ngSwitchDefault>No access.</p>
</div>
```

Depending on the value of user.role, a different paragraph will be displayed

### 5.7. *ngIf; else

This is a variation of *ngIf that allows you to specify an alternative template to show if the condition is false

Example:

```html
<div *ngIf="dataLoaded; else loading">
  Data is loaded!
</div>

<ng-template #loading>
  Loading, please wait...
</ng-template>
```

This example will display "Data is loaded!" if dataLoaded is true. Otherwise, it will show "Loading, please wait..." using the loading template

These directives enhance Angular's HTML template capabilities, allowing developers to build more interactive, dynamic, and conditional UI elements directly within their HTML templates, promoting clean and maintainable code

### 5.8. [(ngModel)]

This is a two-way data binding directive from the FormsModule

It allows you to bind HTML form elements to component data properties

Example:

```html
<input [(ngModel)]="user.name" type="text">
```

This input field is bound to the user.name property. Any changes in the input field will immediately update the user.name property and vice versa

### 5.9. [ngClass] and [ngStyle]

These directives are used to dynamically set CSS classes and styles

Examples for [ngClass]:

```html
<div [ngClass]="{'highlight': isHighlighted, 'error': hasError}">Content</div>
```

```html
<div [ngClass]="{
  'active': isActive,
  'disabled': isDisabled,
  'visible': isVisible
}">Multiple conditional classes</div>
```

This div will have the highlight class if isHighlighted is true and the error class if hasError is true

Examples for [ngStyle]:

```html
<div [ngStyle]="{'font-size': size + 'px', 'color': color}">Styled content</div>
```

```html
<div [ngStyle]="{
  'background-color': isActive ? 'green' : 'red',
  'border-style': isVisible ? 'solid' : 'dashed'
}">Dynamic styles based on conditions</div>
```

This div will have its font size and color set based on the size and color properties

### 5.10. *ngTemplateOutlet

This directive is used to render embedded views loaded from an ng-template

Example:

```html
<ng-template #myTemplate let-description="description">
  <div>{{ description }}</div>
</ng-template>

<div *ngTemplateOutlet="myTemplate; context: {$implicit: 'This is a dynamic description'}"></div>
```

This example shows how to use a template with a context, passing a dynamic description to the template

### 5.11. *ngLet

The *ngLet directive allows you to store a value in a variable within the template context

This is especially useful when you want to cache the result of an expression, so you don't need to recalculate it multiple times within the same template

Example:

```html
<ng-container *ngLet="complexCalculation() as result">
  <div>{{ result }}</div>
  <div>The result is {{ result > 0 ? 'positive' : 'negative' }}</div>
</ng-container>
```

In this example, complexCalculation() is called only once, and its result is reused in multiple places in the template

### 5.12. [ngValue]

This directive is used primarily with ```<select>``` elements to bind the value property to non-string data types

This is useful when you want to bind the selected option to a complex object instead of a string

Example:

```html
<select [(ngModel)]="selectedOption">
  <option *ngFor="let option of options" [ngValue]="option">{{ option.label }}</option>
</select>
```

Here, each option in the options array can be a complex object, and selectedOption will be set to the selected object when an option is chosen

### 5.13. [ngPlural]

**ngPlural** is a directive that provides a way to control content based on pluralization rules

It’s particularly useful in applications supporting multiple languages and needing to properly handle singular vs. plural forms based on dynamic content

Example:

```html
<ng-container [ngPlural]="items.length">
  <ng-template ngPluralCase="=0">No items.</ng-template>
  <ng-template ngPluralCase="=1">One item.</ng-template>
  <ng-template ngPluralCase="other">{{ items.length }} items.</ng-template>
</ng-container>
```

This setup will display different messages based on the number of items in the array.

### 5.14. Custom Directive

**Directives** are classes that add additional behavior to elements in your Angular applications

Apart from **built-in directives** like: **ng-content**, **ng-template**, **ng-container**, **ngIf**, **ngFor**, etc, you can create **custom directives**

Here’s an example of a custom attribute directive that changes the background color of an element:

**highlight.directive.ts**

```typescript
import { Directive, ElementRef, Input, OnInit } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective implements OnInit {
  @Input() appHighlight: string;

  constructor(private el: ElementRef) {}

  ngOnInit() {
    this.el.nativeElement.style.backgroundColor = this.appHighlight || 'yellow';
  }
}
```

Usage in a component template:

**app.component.html**

```html
<p [appHighlight]="'lightgreen'">Highlighted text!</p>
```

Custom directives allow you to write your own directive to encapsulate complex behavior in a way that's reusable across multiple components or modules. There are mainly two types:

**Attribute Directives**

Change the appearance or behavior of an element, component, or another directive

For example, you could create a directive that changes the format of text or handles complex mouse events

**Example: Tooltip Directive**

```typescript
import { Directive, ElementRef, HostListener, Input } from '@angular/core';

@Directive({
  selector: '[appTooltip]'
})
export class TooltipDirective {
  @Input('appTooltip') tooltipText: string;

  constructor(private el: ElementRef) {}

  @HostListener('mouseenter') onMouseEnter() {
    // logic to show tooltip
    this.el.nativeElement.title = this.tooltipText;
  }

  @HostListener('mouseleave') onMouseLeave() {
    // logic to hide tooltip
    this.el.nativeElement.title = '';
  }
}
```

Usage in HTML:

```html
<button appTooltip="Click to perform an action">Hover over me!</button>
```

## 6. Angular Modules

Modules in Angular help organize an application into cohesive blocks of functionality

Here’s an example of a feature module:

```typescript
// books.module.ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { BooksListComponent } from './books-list/books-list.component';

@NgModule({
  declarations: [BooksListComponent],
  imports: [CommonModule],
  exports: [BooksListComponent]
})
export class BooksModule {}
```

## 7. Lazy Loading

Lazy loading is a technique in Angular to load modules only when they are needed

This can significantly improve the startup time of your application

Here's how to configure lazy loading in Angular's routing:

```typescript
// app-routing.module.ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

const routes: Routes = [
  {
    path: 'books',
    loadChildren: () => import('./books/books.module').then(m => m.BooksModule)
  }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

## 8. Change Detection Strategies

Angular provides two change detection strategies: **Default** and **OnPush**

**OnPush** can improve performance by reducing the checks Angular performs. 

Here’s how to use OnPush:

```typescript
// user.component.ts
import { Component, Input, ChangeDetectionStrategy } from '@angular/core';
import { User } from './user.model';  // Assume a model interface is defined

@Component({
  selector: 'app-user',
  template: `<p>{{ user.name }}</p>`,
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class UserComponent {
  @Input() user: User;
}
```

This component will now only check for and react to changes when its input properties change, rather than checking during every change detection cycle

Let's explore additional advanced Angular features such as Interceptors, State Management with NgRx, Dynamic Components, and Content Projection

These features enable sophisticated handling of various application needs such as state control, dynamic behavior, and efficient data handling

## 9.  HTTP Interceptors

Interceptors provide a way to intercept and modify HTTP requests and responses in your Angular applications

They can be used for logging, caching, or adding custom headers

Here’s how you might create an interceptor for adding an authentication token to outgoing requests:

```typescript
// auth.interceptor.ts
import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable()
export class AuthInterceptor implements HttpInterceptor {

  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const authToken = this.getAuthToken();
    const authReq = req.clone({
      headers: req.headers.set('Authorization', `Bearer ${authToken}`)
    });
    return next.handle(authReq);
  }

  private getAuthToken(): string {
    // Retrieve the user's token from storage
    return 'your_token_here';
  }
}
```

**Register the interceptor in your module**:

```typescript
// app.module.ts
import { HTTP_INTERCEPTORS } from '@angular/common/http';
import { AuthInterceptor } from './auth.interceptor';

@NgModule({
  // Other module properties
  providers: [
    { provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi: true }
  ]
})
export class AppModule {}
```

## 10. State Management with NgRx

**NgRx** is a framework for building reactive applications in Angular using the Redux pattern

Here is a simple example of setting up NgRx for managing the state of user data:

```typescript
// actions/user.actions.ts
import { createAction, props } from '@ngrx/store';
import { User } from '../models/user.model';

export const addUser = createAction(
  '[User List] Add User',
  props<{ user: User }>()
);
```

```typescript
// reducers/user.reducer.ts
import { createReducer, on } from '@ngrx/store';
import { addUser } from '../actions/user.actions';
import { User } from '../models/user.model';

export const initialState: ReadonlyArray<User> = [];

export const userReducer = createReducer(
  initialState,
  on(addUser, (state, { user }) => [...state, user])
);
```

## 11. Dynamic Component Loading

Angular can dynamically load components based on conditions or at runtime

This can be useful for large applications where you want to load components as needed without increasing the initial load time:

```typescript
// dynamic.component.ts
import { Component, Input, OnInit, ViewChild, ComponentFactoryResolver, ViewContainerRef } from '@angular/core';

@Component({
  selector: 'app-dynamic',
  template: `<ng-template #container></ng-template>`
})
export class DynamicComponent implements OnInit {
  @ViewChild('container', { read: ViewContainerRef }) container: ViewContainerRef;
  @Input() childComponent: any;

  constructor(private resolver: ComponentFactoryResolver) {}

  ngOnInit() {
    const factory = this.resolver.resolveComponentFactory(this.childComponent);
    this.container.createComponent(factory);
  }
}
```

## 12. Content Projection

Content projection (transclusion in AngularJS terms) allows you to inject HTML content from the parent component into the child component

Here’s an example using the <ng-content> directive:

```typescript
// panel.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-panel',
  template: `
    <div class="panel">
      <ng-content select="[panel-title]"></ng-content>
      <ng-content select="[panel-body]"></ng-content>
    </div>
  `
})
export class PanelComponent {}
```

// Usage in parent component

```html
<!-- parent.component.html -->
<app-panel>
  <h2 panel-title>Title of Panel</h2>
  <div panel-body>Content of the panel goes here.</div>
</app-panel>
```

## 13. Using Observables and Promises in Angular

Angular integrates **RxJS Observables** extensively for handling asynchronous operations

Here’s an example of using Observables in a service to handle HTTP requests, and an example of **converting an Observable to a Promise** in a component

**Service using Observable**:

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';
import { map } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  constructor(private http: HttpClient) {}

  fetchData(): Observable<any> {
    return this.http.get('https://api.example.com/data')
      .pipe(
        map(response => response.data)
      );
  }
}
```

**Component using Promises**:

```typescript
import { Component, OnInit } from '@angular/core';
import { DataService } from './data.service';

@Component({
  selector: 'app-example',
  template: `<div>{{ data | json }}</div>`
})
export class ExampleComponent implements OnInit {
  data: any;

  constructor(private dataService: DataService) {}

  ngOnInit() {
    this.dataService.fetchData().toPromise().then(data => {
      this.data = data;
    }).catch(error => {
      console.error('Error fetching data:', error);
    });
  }
}
```

## 14. Pipes in Angular

### 14.1.  Built-in Pipes in Angular


Angular provides several built-in pipes that help you transform data right in your templates

Pipes are simple functions you can use in template expressions to accept an input value and return a transformed value

Here's an overview of some of the most commonly used built-in pipes in Angular, complete with examples for each:

#### 14.1.1. DatePipe

Transforms a date value according to locale rules and parameters you provide for formatting

```html
<p>{{ today | date:'fullDate' }}</p>
<!-- Output might look like: "Sunday, June 28, 2020" -->
```

2. UpperCasePipe and LowerCasePipe

Transforms text to all upper or lower case.

```html
<p>{{ 'Hello World' | uppercase }}</p> <!-- HELLO WORLD -->
<p>{{ 'Hello World' | lowercase }}</p> <!-- hello world -->
```

3. CurrencyPipe

Transforms a number to a currency string, formatted according to locale rules.

```html
<p>{{ 1234.5 | currency:'USD':'symbol':'1.2-2' }}</p>
<!-- Output might look like: "$1,234.50" -->
```

4. DecimalPipe

Transforms a number into a decimal number string, formatted according to locale rules.

```html
<p>{{ 1.3495 | number:'1.1-2' }}</p>
<!-- Output: "1.35" -->
```

5. PercentPipe

Transforms a number to a percent string, formatted according to locale rules.

```html
<p>{{ 0.154 | percent:'1.0-2' }}</p>
<!-- Output: "15.40%" -->
```

6. SlicePipe

Creates a new Array or String containing a subset (slice) of the elements

```html
<p>{{ 'Hello' | slice:1:3 }}</p> <!-- "el" -->
<p>{{ [1, 2, 3, 4, 5] | slice:1:3 }}</p> <!-- [2,3] -->
```

7. JsonPipe

Converts a value into its JSON-format string. Useful for debugging.

```html
<p>{{ {name: 'John'} | json }}</p>
<!-- Output: '{"name": "John"}' -->
```

8. AsyncPipe

Automatically subscribes to an Observable or Promise and returns the latest value it has emitted.

```html
<p>{{ userObservable | async }}</p>
```

9. KeyValuePipe

Converts an object or Map into an array of key-value pairs so you can iterate over it with *ngFor.

```html
<div *ngFor="let item of object | keyvalue">
  {{item.key}}:{{item.value}}
</div>
```

10. TitleCasePipe

Transforms the first letter of each word to uppercase; other letters remain unchanged.

```html
<p>{{ 'hello world' | titlecase }}</p> <!-- "Hello World" -->
```

These pipes are powerful tools for formatting and displaying data in your Angular applications, allowing you to keep your component code clean and focused on business logic, while the template handles the display logic. Each pipe is designed to be used in template expressions, making them both convenient and efficient for transforming data directly in the UI layer



### 14.2.  Custom Pipes for Data Transformatio

Angular pipes are used for transforming output in templates

You can create custom pipes to perform specific transformations

**Creating a Custom Pipe**:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'capitalize'
})
export class CapitalizePipe implements PipeTransform {
  transform(value: string): string {
    if (value) {
      return value.charAt(0).toUpperCase() + value.slice(1);
    }
    return value;
  }
}
```

**Using the Pipe in a Template**:

```html
<!-- In some component template -->
<p>{{ 'hello' | capitalize }}</p>
```

## 15. Route Guards

Route guards are used in Angular to decide if a user can navigate to or leave a certain route

Here’s an example of using a route guard for authentication

**Creating a Route Guard**:

```typescript
import { Injectable } from '@angular/core';
import { CanActivate, Router, ActivatedRouteSnapshot, RouterStateSnapshot } from '@angular/router';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  constructor(private router: Router) {}

  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): boolean {
    if (localStorage.getItem('currentUser')) {
      return true;
    } else {
      this.router.navigate(['/login'], { queryParams: { returnUrl: state.url }});
      return false;
    }
  }
}
```

**Using the Guard in Routing**:

```typescript
import { Routes } from '@angular/router';
import { AuthGuard } from './auth.guard';
import { HomeComponent } from './home.component';
import { LoginComponent } from './login.component';

const routes: Routes = [
  { path: 'home', component: HomeComponent, canActivate: [AuthGuard] },
  { path: 'login', component: LoginComponent }
];
```

## 16. Decorators

Decorators are a design pattern that is used to separate modification or decoration of a class without modifying the original source code

**Creating a Custom Decorator**:

```typescript
function Log(target: any, propertyName: string | Symbol) {
  let value = target[propertyName];

  const getter = () => {
    console.log(`Get: ${propertyName} => ${value}`);
    return value;
  };

  const setter = (newValue: any) => {
    console.log(`Set: ${propertyName} => ${newValue}`);
    value = newValue;
  };

  Object.defineProperty(target, propertyName, {
    get: getter,
    set: setter
  });
}

class MyClass {
  @Log
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}
```
