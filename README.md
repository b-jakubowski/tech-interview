# Tech-Interview-Questions

## Table of Contents
Architecture:
* [Model-View-Presenter with Angular](#model-view-presenter-with-angular)
* [Component based architecture](#component-based-architecture)
* [Dependency injection](#dependency-injection)
* [Unidirectional data flow](#dependency-injection)
* [Centralized state management](#centralized-state-management)

General:
* [Components life-cycle hooks](#Components-life-cycle-hooks)
* [One-way and Two-way Data Binding in Angular](#one-way-and-two-way-data-binding-in-angular)

Routes:
* [Route Guards](#route-guards)
* [CanDeactivate guard](#candeactivate-guard)

RxJS:
* [Reactive programming](#reactive-programming)
* [Subject vs BehaviorSubject](#subject-vs-behaviorsubject)

NgRx:
* [What is NgRx](#what-is-ngrxs)

TypeScript: 
* [TypeScript inference type](#typescript-inference-type)


## Architecture:
### Model-View-Presenter with Angular
[More details](https://blog.angularindepth.com/model-view-presenter-with-angular-3a4dbffe49bb)
* Model-View-Presenter (often abbreviated MVP) is an architectural software design pattern for implementing the user interface (UI) of an application.
* Model-View-Presenter separates presentation from the domain model
* The presentation layer reacts to changes in the domain by applying the Observer Pattern
* The view does not contain any logic or behaviour except in the form of data bindings and widget composition. It delegates control to a presenter when user interactions occur.
* The presenter batches state changes so that the user filling a form results in one big state change as opposed to many small changes, e.g. update the application state once per form instead of once per field.

Components in that case can be divided :
- Presentational components - purely presentational and interactive views. They present a piece of the application state to the user and enable them to affect its state. keep the complexity of presentational components to an absolute minimum
- Container components - expose pieces of application state to presentational components. They integrate the presentational layer with the rest of our application by translating component-specific events to commands and queries for non-presentational layers.
- Mixed components -  they contain logic that belongs in multiple horizontal layers. complicated to reuse and tightly coupled.
![M-V-P](https://miro.medium.com/max/875/1*ZbBBKiBXGqVBYWwzbmZzNw.png "mvp")

### Component based architecture:
* Container components supply a data flow for presentation.
* Container components translate component-specific events to application state commands or actions to put it in Redux/NgRx Store terms.

### Dependency injection
* Dependency injection (DI) lets you keep your component classes lean and efficient. They don't fetch data from the server, validate user input, or log directly to the console; they delegate such tasks to services.
* Podstawową zasadą działania Dependency Injection jest posiadanie serwisu, który zajmuje się uzupełnianiem potrzebnych zależności.

### Unidirectional data flow
change detection cannot cause cycles. It also helps to maintain simpler and more predictable data flows in applications, along with substantial performance improvements.
![unidirectional data flow](https://miro.medium.com/max/875/1*kwcTqvUDyhsPJU_Bbl4C6g.png "unidirectional data flow")

### Centralized state management
- The application state is a single immutable data structure
- A state change is triggered by an action, an object describing what happened
- Pure functions called reducers take the previous state and the next action to compute the new state

![state](https://miro.medium.com/max/875/1*KGK4Je5Iq7GrUPXz-XePzw.png "state")

## General

### Angular Performance Checklist
[Angular Performance Checklist](https://github.com/mgechev/angular-performance-checklist)
TLDR:
- OnPush strategy
- Angular Zone optimization
- manually set changeDetection
- @Input as setter instead OnChanges hook
- lazy loading of views / modules

### Server-side rendering
A normal Angular application executes in the browser, rendering pages in the DOM in response to user actions. Angular Universal executes on the server, generating static application pages that later get bootstrapped on the client. 
Big issue of the traditional SPA is that they cannot be rendered until the entire JavaScript required for their initial rendering is available. This leads to two big problems:

Not all search engines are running the JavaScript associated to the page so they are not able to index the content of dynamic apps properly.
Poor user experience, since the user will see nothing more than a blank/loading screen until the JavaScript associated with the page is downloaded, parsed and executed.

Server-side rendering solves this issue by pre-rendering the requested page on the server and providing the markup of the rendered page during the initial page load.

### Components life-cycle hooks
* ngOnChanges() - Called before ngOnInit() and whenever one or more data-bound input properties change.
* ngOnInit() - Called once, after the first ngOnChanges().
* ngDoCheck() - Called during every change detection run, immediately after ngOnChanges() and ngOnInit().
* ngAfterContentInit() - Called once after the first ngDoCheck().
* ngAfterContentChecked() - Called after the ngAfterContentInit() and every subsequent ngDoCheck().
* ngAfterViewInit() - Called once after the first ngAfterContentChecked().
* ngAfterViewChecked() - Called after the ngAfterViewInit() and every subsequent ngAfterContentChecked().
* ngOnDestroy() - Called just before Angular destroys the directive/component.

### One-way and Two-way Data Binding in Angular
* One-way data binding will bind the data from the component to the view (DOM) or from view to the component. One-way data binding is unidirectional.
* Two-way data binding in Angular will help users to exchange data from the component to view and from view to the component. It will help users to establish communication bi-directionally.
* Why not 2-way-binding - what you lose in return is the ability to control when state should change and sight of where changes come from. Also when the application grows on size, the performance may decrease because angular will watch of every 2waybinding element.

## Rxjs
### Reactive programming: 
Angular uses RxJS to implement the Observable pattern.
An Observable is a stream of asynchronous events that can be processed with array-like operators.
- An Observer essentially subscribes to an Observable.
- The Observable then emits streams of data which the Observer listens and reacts to, setting in motion a chain of operations on the data stream.
- Operators allow you to transform, combine, manipulate, and work with the sequences of items emitted by Observables.

### Subject vs BehaviorSubject
A BehaviorSubject holds one value. When it is subscribed it emits the value immediately. A Subject doesn't hold a value.
- BehaviorSubject can be created with initial value: new BehaviorSubject(1)
- Consider ReplaySubject if you want the subject to hold more than one value

Subject example ():
```
const subject = new Subject();
subject.next(1);
subject.subscribe(x => console.log(x));
```
Console output will be empty

BehaviorSubject example:
```
const subject = new BehaviorSubject();
subject.next(1);
subject.subscribe(x => console.log(x));
```
Console output: 1

## NgRx
### What is NgRx?


## Routing
### Route Guards
* **CanActivate**: Controls if a route can be activated.
* **CanActivateChild**: Controls if children of a route can be activated.
* **CanLoad**: Controls if a route can even be loaded. This becomes useful for feature modules that are lazy loaded. They won’t even load if the guard returns false.
* **CanDeactivate**: Controls if the user can leave a route. Note that this guard doesn’t prevent the user from closing the browser tab or navigating to a different address. It only prevents actions from within the application itself.

### CanDeactivate guard

### TypeScript inference type
If you add value to initialized variable, there is no need to provide type to it
```
const x = 1;
```
there is no need to add `number` type to this case.