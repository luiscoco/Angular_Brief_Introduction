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

Angular supports different types of data binding, such as property binding, event binding, and two-way binding. Here’s an example:

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

**Directives** are classes that add additional behavior to elements in your Angular applications

Apart from built-in directives like **ngIf** and **ngFor**, you can create **custom directives**\

Here’s an example of a custom attribute directive that changes the background color of an element:

```typescript
// highlight.directive.ts
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

```html
<!-- app.component.html -->
<p [appHighlight]="'lightgreen'">Highlighted text!</p>
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

This component will now only check for and react to changes when its input properties change, rather than checking during every change detection cycle.
