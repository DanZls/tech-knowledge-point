# Angular

## Contents
- [What is a Module, and what does it contain?](#what-is-a-module-and-what-does-it-contain)
- [What is a Component, and what is its minimum definition?](#what-is-a-component-and-what-is-its-minimum-definition)
- [What's the difference between an Angular Component and Module?](#whats-the-difference-between-an-angular-component-and-module)
- [What is the difference between @Component and @Directive in Angular?](#what-is-the-difference-between-component-and-directive-in-angular)
- [What is a Service, and when will you use it?](#what-is-a-service-and-when-will-you-use-it)
- [What is Interpolation?](#what-is-interpolation)
- [What is the difference between Structural and Attribute directives in Angular?](#what-is-the-difference-between-structural-and-attribute-directives-in-angular)
- [What is a bootstrapping module?](#what-is-a-bootstrapping-module)
- [What is the purpose of base href tag, and how do you inject base href?](#what-is-the-purpose-of-base-href-tag-and-how-do-you-inject-base-href)
- [What are the differences between AngularJS (angular 1.x) and Angular (Angular 2.x and beyond)?](#what-are-the-differences-between-angularjs-angular-1x-and-angular-angular-2x-and-beyond)
- [What is a Routing Guard in Angular, and how would you protect a component being activated through the router?](#what-is-a-routing-guard-in-angular-and-how-would-you-protect-a-component-being-activated-through-the-router)
- [What is Router Outlet?](#what-is-router-outlet)
- [What is Router State?](#what-is-router-state)
- [What is Activated route?](#what-is-activated-route)
- [What is the purpose of Wildcard route?](#what-is-the-purpose-of-wildcard-route)
- [Do I always need a Routing Module?](#do-i-always-need-a-routing-module)
- [What is the equivalent of ngShow and ngHide in Angular?](#what-is-the-equivalent-of-ngshow-and-nghide-in-angular)
- [What is the difference between *ngIf vs [hidden]?](#what-is-the-difference-between-ngif-vs-hidden)
- [You have an HTML response you want to display. How do you do that safely in Angular?](#you-have-an-html-response-you-want-to-display-how-do-you-do-that-safely-in-angular)
- [What are Pipes? Give an example.](#what-are-pipes-give-an-example)
- [What is a Parameterized pipe?](#what-is-a-parameterized-pipe)
- [What is the difference between pure and impure pipe?](#what-is-the-difference-between-pure-and-impure-pipe)
- [How can I select an element in a component template?](#how-can-i-select-an-element-in-a-component-template)
- [What does this line do?](#what-does-this-line-do)
- [What is an Observable?](#what-is-an-observable)
- [What is an Observer?](#what-is-an-observer)
- [What is Subscribing?](#what-is-subscribing)
- [What is Multicasting?](#what-is-multicasting)
- [What are observable creation functions?](#what-are-observable-creation-functions)
- [What is the difference between Promise and Observable in Angular, and when would you use each?](#what-is-the-difference-between-promise-and-observable-in-angular-and-when-would-you-use-each)
- [What is the difference between BehaviorSubject and Observable?](#what-is-the-difference-between-behaviorsubject-and-observable)
- [How do you perform error handling in Observables?](#how-do-you-perform-error-handling-in-observables)
- [What are the utility functions/operators provided by RxJS?](#what-are-the-utility-functionsoperators-provided-by-rxjs)
- [What is Reactive Programming and how does it relate to Angular?](#what-is-reactive-programming-and-how-does-it-relate-to-angular)
- [What is the difference between declarations, providers, and imports in NgModule?](#what-is-the-difference-between-declarations-providers-and-imports-in-ngmodule)
- [Explain the difference between constructor and ngOnInit. Why use ngOnInit if a constructor already exists?](#explain-the-difference-between-constructor-and-ngoninit-why-use-ngoninit-if-a-constructor-already-exists)
- [What are the lifecycle hooks for components and directives?](#what-are-the-lifecycle-hooks-for-components-and-directives)
- [How do you categorize data binding types?](#how-do-you-categorize-data-binding-types)
- [What happens if you use a `script` tag inside an Angular template?](#what-happens-if-you-use-a-script-tag-inside-an-angular-template)
- [How do you choose between an inline and external template file?](#how-do-you-choose-between-an-inline-and-external-template-file)
- [How would you run unit tests in Angular?](#how-would-you-run-unit-tests-in-angular)
- [What is TestBed?](#what-is-testbed)
- [Why would you use a spy in a test?](#why-would-you-use-a-spy-in-a-test)
- [What does detectChanges do in Angular Jasmine tests?](#what-does-detectchanges-do-in-angular-jasmine-tests)
- [How do you create an application to use SCSS?](#how-do-you-create-an-application-to-use-scss)
- [How do you bundle an Angular app for production?](#how-do-you-bundle-an-angular-app-for-production)
- [How do you set headers for every request in Angular?](#how-do-you-set-headers-for-every-request-in-angular)
- [How do you perform error handling for HttpClient?](#how-do-you-perform-error-handling-for-httpclient)
- [Could I use jQuery with Angular?](#could-i-use-jquery-with-angular)
- [What is Redux and how does it relate to an Angular app?](#what-is-redux-and-how-does-it-relate-to-an-angular-app)
- [What are dynamic components?](#what-are-dynamic-components)
- [What are Custom Elements in Angular, how do they work internally, and do they need bootstrapping?](#what-are-custom-elements-in-angular-how-do-they-work-internally-and-do-they-need-bootstrapping)
- [What are the mapping rules between an Angular component and a custom element?](#what-are-the-mapping-rules-between-an-angular-component-and-a-custom-element)
- [How can you run AngularJS and Angular side by side (ngUpgrade)?](#how-can-you-run-angularjs-and-angular-side-by-side-ngupgrade)
- [Is there an equivalent to $scope.emit() or $scope.broadcast() in Angular?](#is-there-an-equivalent-to-scopeemit-or-scopebroadcast-in-angular)
- [How would you control the size of an element on window resize in a component?](#how-would-you-control-the-size-of-an-element-on-window-resize-in-a-component)
- [What is Zone/NgZone in Angular, and when would you use it?](#what-is-zonengzone-in-angular-and-when-would-you-use-it)
- [What is the Angular equivalent of an AngularJS $watch?](#what-is-the-angular-equivalent-of-an-angularjs-watch)
- [Why would you use renderer methods instead of native element methods?](#why-would-you-use-renderer-methods-instead-of-native-element-methods)
- [How would you insert an embedded view from a prepared TemplateRef?](#how-would-you-insert-an-embedded-view-from-a-prepared-templateref)
- [Name and explain Angular module loading strategies.](#name-and-explain-angular-module-loading-strategies)
- [When would you use eager loading?](#when-would-you-use-eager-loading)
- [What is lazy loading in Angular, why use it, and when is a lazy-loaded module loaded?](#what-is-lazy-loading-in-angular-why-use-it-and-when-is-a-lazy-loaded-module-loaded)
- [What is the need for SystemJS in Angular?](#what-is-the-need-for-systemjs-in-angular)
- [What are key differences between SystemJS and webpack?](#what-are-key-differences-between-systemjs-and-webpack)
- [How would you extract webpack config from an Angular CLI project?](#how-would-you-extract-webpack-config-from-an-angular-cli-project)
- [Why do we need a compilation process in Angular?](#why-do-we-need-a-compilation-process-in-angular)
- [What does a just-in-time (JIT) compiler do?](#what-does-a-just-in-time-jit-compiler-do)
- [What is AOT, what are its advantages, and how is it different from JIT?](#what-is-aot-what-are-its-advantages-and-how-is-it-different-from-jit)
- [What are ways to control AOT compilation?](#what-are-ways-to-control-aot-compilation)
- [What is Angular Ivy?](#what-is-angular-ivy)
- [What is Ivy Renderer?](#what-is-ivy-renderer)
- [How would you compare View Engine vs Ivy?](#how-would-you-compare-view-engine-vs-ivy)
- [What is the Locality principle in Ivy?](#what-is-the-locality-principle-in-ivy)
- [How does Ivy affect rebuild time?](#how-does-ivy-affect-rebuild-time)
- [What is Incremental DOM, and how is it different from Virtual DOM?](#what-is-incremental-dom-and-how-is-it-different-from-virtual-dom)
- [Why does Incremental DOM have a low memory footprint and support tree shaking?](#why-does-incremental-dom-have-a-low-memory-footprint-and-support-tree-shaking)
- [Why did the Google team choose Incremental DOM instead of Virtual DOM?](#why-did-the-google-team-choose-incremental-dom-instead-of-virtual-dom)
- [Explain the purpose of Service Workers in Angular.](#explain-the-purpose-of-service-workers-in-angular)
- [What is Angular Universal?](#what-is-angular-universal)
- [What is Protractor?](#what-is-protractor)
- [What is Bazel, and why would you use it for Angular builds?](#what-is-bazel-and-why-would-you-use-it-for-angular-builds)
- [What is the use of Codelyzer?](#what-is-the-use-of-codelyzer)
- [Name some security best practices in Angular.](#name-some-security-best-practices-in-angular)
- [What are pros/cons (especially performance-wise) of using local storage to replace cookies?](#what-are-proscons-especially-performance-wise-of-using-local-storage-to-replace-cookies)
- [How do you detect a route change in Angular?](#how-do-you-detect-a-route-change-in-angular)
- [When do you use query parameters versus matrix parameters in URL?](#when-do-you-use-query-parameters-versus-matrix-parameters-in-url)
- [Why does Angular use URL segments?](#why-does-angular-use-url-segments)
- [Angular 9: What are some new features?](#angular-9-what-are-some-new-features)
- [Angular 9: Explain improvements in tree-shaking.](#angular-9-explain-improvements-in-tree-shaking)
- [Angular 8: What are some changes in the Location module?](#angular-8-what-are-some-changes-in-the-location-module)

---

## What is a Module, and what does it contain?
An Angular module is a logical container that groups related building blocks of an app. It helps organize features by bundling components, directives, pipes, and services together. A module can also import other modules to reuse functionality and export selected pieces for other modules. In modern Angular, standalone APIs reduce module usage, but NgModules are still common in many codebases and interviews. A typical module contains declarations, imports, providers, and optionally bootstrap information.

```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  providers: [LoggerService],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

---

## What is a Component, and what is its minimum definition?
A component is the main UI unit in Angular and controls one part of the screen. It combines template, logic, and metadata into a reusable block. The minimum practical definition is a class plus a `@Component` decorator with at least a selector and template. Components can receive input, emit output, and participate in lifecycle hooks. Angular renders a component wherever its selector appears in HTML.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-hello',
  template: '<p>Hello Angular</p>'
})
export class HelloComponent {}
```

---

## What's the difference between an Angular Component and Module?
A component is a visual building block, while a module is an organizational boundary. Components define UI behavior and templates for a specific view fragment. Modules group components and related code so Angular knows how parts fit together. You render components in templates, but modules are not rendered directly. Think of modules as packaging and components as display units.

```ts
@NgModule({ declarations: [ProfileComponent] })
export class ProfileModule {}

@Component({ selector: 'app-profile', template: '<h2>Profile</h2>' })
export class ProfileComponent {}
```

---

## What is the difference between @Component and @Directive in Angular?
`@Component` is a specialized directive that always has a template and is meant to render UI. `@Directive` adds behavior to existing elements without owning a template. Components typically use a selector as a custom tag, while directives often use attribute selectors. Both can use dependency injection, inputs, outputs, and lifecycle hooks. In short, every component is a directive, but not every directive is a component.

```ts
@Directive({ selector: '[appHighlight]' })
export class HighlightDirective {}

@Component({ selector: 'app-card', template: '<div>Card</div>' })
export class CardComponent {}
```

---

## What is a Service, and when will you use it?
A service is a class that holds reusable business logic or shared state outside components. You use services to avoid duplicating code across multiple components. Common use cases include HTTP calls, caching, logging, and cross-component communication. Services are created through dependency injection, which improves testability and modularity. You should keep components lean by delegating non-UI logic to services.

```ts
@Injectable({ providedIn: 'root' })
export class UserService {
  getUserName(): string {
    return 'Alice';
  }
}
```

---

## What is Interpolation?
Interpolation is Angular template syntax that inserts component values into HTML using `{{ }}`. It is one-way binding from component class to template. Angular evaluates the expression and keeps the UI updated when data changes. Interpolation is commonly used for text, not for setting complex object attributes directly. It is simple, readable, and ideal for displaying dynamic values.

```html
<h1>{{ title }}</h1>
<p>User: {{ user.name }}</p>
```

---

## What is the difference between Structural and Attribute directives in Angular?
Structural directives change DOM structure by adding or removing elements. Attribute directives change appearance or behavior of existing elements without removing them. Structural directives are used with `*` syntax, such as `*ngIf` and `*ngFor`. Attribute directives include examples like `[ngClass]`, `[ngStyle]`, or custom hover effects. Use structural directives for layout control and attribute directives for style/behavior adjustments.

```html
<div *ngIf="isLoggedIn">Welcome</div>
<div [ngClass]="{ active: isLoggedIn }">Status</div>
```

---

## What is a bootstrapping module?
The bootstrapping module is the root module Angular uses to start the application. In classic setups, this is usually `AppModule`. It tells Angular which root component should be created first. During bootstrap, Angular initializes dependency injection, compiles templates, and mounts the app into the DOM. In standalone setups, bootstrapping happens with `bootstrapApplication()` instead of an NgModule.

```ts
platformBrowserDynamic()
  .bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

---

## What is the purpose of base href tag, and how do you inject base href?
The `<base href="/">` tag defines the root URL for relative links in the app. Angular Router uses it to build client-side navigation paths correctly. If base href is wrong, deep links and asset URLs can break, especially in subfolder deployments. You can inject it via `APP_BASE_HREF` when you need custom routing base at runtime. This is useful for hosting app versions under different paths.

```ts
import { APP_BASE_HREF } from '@angular/common';

providers: [{ provide: APP_BASE_HREF, useValue: '/my-app/' }]
```

---

## What are the differences between AngularJS (angular 1.x) and Angular (Angular 2.x and beyond)?
AngularJS is JavaScript-based with MVC-style patterns and heavy `$scope` usage. Angular (2+) is TypeScript-first, component-based, and built around classes and decorators. Angular uses a more powerful compiler, RxJS, and modern tooling via CLI. Performance, maintainability, and testability are significantly better in Angular compared to AngularJS. AngularJS uses dirty checking, while Angular uses unidirectional data flow with change detection strategies.

```ts
// Angular (2+) component style
@Component({ selector: 'app-root', template: '<h1>Hello</h1>' })
export class AppComponent {}
```

---

## What is a Routing Guard in Angular, and how would you protect a component being activated through the router?
A route guard controls navigation based on conditions like authentication or role checks. The most common guard for protecting route activation is `CanActivate`. You implement guard logic in a service and return `boolean`, `UrlTree`, `Promise`, or `Observable`. If unauthorized, you can redirect users to login instead of loading the component. This keeps access control centralized and consistent.

```ts
@Injectable({ providedIn: 'root' })
export class AuthGuard implements CanActivate {
  canActivate(): boolean | UrlTree {
    return this.auth.isLoggedIn() ? true : this.router.parseUrl('/login');
  }
}
```

---

## What is Router Outlet?
`<router-outlet>` is a placeholder where Angular injects routed components. It acts like a dynamic view container controlled by the router. When route changes, Angular replaces the active component inside the outlet. You can have nested outlets for child routes and layout hierarchies. Without a router outlet, route components have nowhere to render.

```html
<nav><a routerLink="/home">Home</a></nav>
<router-outlet></router-outlet>
```

---

## What is Router State?
Router state is a tree representing the current activated routes in the app. It includes URL segments, route params, query params, data, and component hierarchy. Angular updates this state on each successful navigation. You can inspect it to determine where the user is and what data is available. It is useful for breadcrumbs, access logic, and debugging navigation flow.

```ts
constructor(private router: Router) {
  console.log(this.router.routerState.snapshot.url);
}
```

---

## What is Activated route?
`ActivatedRoute` gives access to information about the currently matched route for a component. It exposes params, query params, static data, and URL segments as observables. You typically inject it into routed components to read route context. Use `snapshot` for one-time reads or observables for reacting to changes. It is essential when a component is reused across different parameter values.

```ts
constructor(private route: ActivatedRoute) {}

ngOnInit(): void {
  this.route.params.subscribe(p => console.log(p['id']));
}
```

---

## What is the purpose of Wildcard route?
A wildcard route (`**`) catches unmatched URLs in your routing configuration. It is usually used to show a 404 page or redirect to a safe route. Angular checks routes top-down, so wildcard should be last. If placed too early, it can block valid routes. It improves UX by handling invalid links gracefully.

```ts
const routes: Routes = [
  { path: 'home', component: HomeComponent },
  { path: '**', component: NotFoundComponent }
];
```

---

## Do I always need a Routing Module?
You do not always need a separate routing module, especially in small or standalone apps. Routes can be declared directly in the root module or provided via `provideRouter`. However, a dedicated routing module improves separation of concerns in medium or large projects. It keeps route config centralized and easier to maintain. So it is optional technically, but often a good architectural practice.

```ts
bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes)]
});
```

---

## What is the equivalent of ngShow and ngHide in Angular?
Angular does not have direct `ngShow/ngHide` directives from AngularJS. Equivalent behavior is achieved using `[hidden]` or CSS class toggling. If you need DOM removal, use `*ngIf` instead of hiding. `[hidden]` keeps element in DOM but sets display behavior via attribute. The right choice depends on performance, lifecycle, and accessibility needs.

```html
<div [hidden]="!isVisible">Visible but still in DOM</div>
<div *ngIf="isVisible">Created/removed from DOM</div>
```

---

## What is the difference between *ngIf vs [hidden]?
`*ngIf` adds or removes elements from the DOM entirely. `[hidden]` only toggles visibility while keeping element and component instance alive. With `*ngIf`, lifecycle hooks run when element is created/destroyed. `[hidden]` is cheaper for frequent toggles when preserving state matters. Use `*ngIf` for conditional existence and `[hidden]` for simple visibility.

```html
<app-editor *ngIf="editMode"></app-editor>
<app-editor [hidden]="!editMode"></app-editor>
```

---

## You have an HTML response you want to display. How do you do that safely in Angular?
By default Angular sanitizes dangerous HTML in `[innerHTML]`, which protects against many XSS risks. You should prefer rendering trusted plain text whenever possible. If HTML must be shown, validate and sanitize it on the server and/or client first. `DomSanitizer.bypassSecurityTrustHtml` should only be used for truly trusted content because it disables safety checks for that value. Never bypass security for user-generated raw HTML without strict controls.

```ts
safeHtml = this.sanitizer.bypassSecurityTrustHtml('<b>Trusted content</b>');

// template
// <div [innerHTML]="safeHtml"></div>
```

---

## What are Pipes? Give an example.
Pipes transform displayed values in templates without changing the source data. Angular has built-in pipes for date, currency, percent, json, and more. You can chain multiple pipes to compose formatting behavior. Custom pipes are useful for reusable presentation transformations. Pipes keep template logic clean and declarative.

```html
<p>{{ amount | currency:'USD' }}</p>
<p>{{ createdAt | date:'mediumDate' }}</p>
```

---

## What is a Parameterized pipe?
A parameterized pipe accepts one or more arguments after the pipe name. Parameters let you customize formatting behavior for each usage. Built-in examples include `date:'short'` and `currency:'EUR':'symbol'`. You can also create custom pipes that take your own parameters. This makes templates expressive while keeping formatting centralized.

```html
<p>{{ birthday | date:'yyyy-MM-dd' }}</p>
<p>{{ price | currency:'EUR':'symbol' }}</p>
```

---

## What is the difference between pure and impure pipe?
Pure pipes run only when Angular detects a pure input reference/value change. They are efficient and ideal for deterministic transformations. Impure pipes run during every change detection cycle, so they can be costly. You use impure pipes only when inputs mutate without reference changes or depend on external state. Prefer pure pipes unless you have a strong reason.

```ts
@Pipe({ name: 'myImpure', pure: false })
export class MyImpurePipe implements PipeTransform {
  transform(value: string[]): string { return value.join(', '); }
}
```

---

## How can I select an element in a component template?
The standard Angular way is using `@ViewChild` or `@ViewChildren`. This avoids direct global DOM querying and keeps code testable. You can reference elements via template reference variables like `#box`. Access is typically available in `ngAfterViewInit`. For DOM operations, prefer Renderer2 when possible for platform safety.

```ts
@ViewChild('box') box!: ElementRef<HTMLDivElement>;

ngAfterViewInit(): void {
  console.log(this.box.nativeElement.offsetWidth);
}
```

---

## What does this line do?
In Angular interviews, this question usually tests whether you can explain code semantics rather than only syntax. A strong answer breaks the line into framework concept, runtime behavior, and side effects. For template bindings, explain data flow direction and update timing. For decorators or RxJS lines, explain metadata registration or stream behavior. Always mention assumptions and context if the exact line is not shown.

```ts
// Example explanation target:
this.route.params.subscribe(params => this.id = params['id']);
// Subscribes to route param changes and updates component state.
```

---

## What is an Observable?
An Observable is a lazy stream that can emit multiple values over time. It supports async data like HTTP, user events, websockets, and timers. Nothing happens until something subscribes to it. Observables can be transformed and combined with RxJS operators. Angular relies on them heavily for reactive patterns.

```ts
const count$ = interval(1000);
count$.subscribe(v => console.log(v));
```

---

## What is an Observer?
An Observer is the consumer that reacts to Observable emissions. It can define handlers for `next`, `error`, and `complete`. You pass an observer object or callbacks into `subscribe`. This design separates data production from data consumption. It makes asynchronous flows explicit and composable.

```ts
const observer = {
  next: (v: number) => console.log(v),
  error: (e: unknown) => console.error(e),
  complete: () => console.log('done')
};
```

---

## What is Subscribing?
Subscribing starts execution of an observable and attaches handlers for emitted events. For cold observables, each subscription runs the producer independently. `subscribe()` returns a Subscription object that can be unsubscribed. Unsubscribing is important to avoid leaks, especially for long-lived streams. In Angular, `async` pipe can handle subscription lifecycle automatically in templates.

```ts
const sub = this.userService.user$.subscribe(u => this.user = u);

ngOnDestroy(): void {
  sub.unsubscribe();
}
```

---

## What is Multicasting?
Multicasting means sharing one observable execution among multiple subscribers. Without multicasting, each subscriber may trigger duplicate work, such as repeated HTTP calls. RxJS operators like `share` and `shareReplay` enable multicasting patterns. Subjects are also commonly used as multicast sources. It improves performance and keeps consumers synchronized.

```ts
const users$ = this.http.get('/api/users').pipe(
  shareReplay(1)
);
```

---

## What are observable creation functions?
Observable creation functions are RxJS helpers that produce observables from values, events, promises, or timers. Common ones include `of`, `from`, `interval`, `timer`, and `fromEvent`. They provide clear intent and avoid manual observable construction in many cases. You can combine them with operators to create rich async flows. Choosing the right creator makes stream code easier to read.

```ts
const a$ = of(1, 2, 3);
const b$ = from(fetch('/api/data'));
const c$ = interval(1000);
```

---

## What is the difference between Promise and Observable in Angular, and when would you use each?
A Promise resolves once and cannot be canceled once started. An Observable can emit many values, can be canceled by unsubscribing, and supports operators. Promise is fine for simple one-shot async tasks. Observable is better for streams, retries, composition, and Angular-native APIs like HttpClient and forms. In Angular apps, Observable is generally preferred for consistency and flexibility.

```ts
const p = fetch('/api/user').then(r => r.json());
const o$ = this.http.get('/api/user');
```

---

## What is the difference between BehaviorSubject and Observable?
An Observable is a general stream abstraction and may not hold current state. A `BehaviorSubject` is both observable and observer, and stores the latest value. New subscribers to BehaviorSubject immediately receive the current value. This makes it useful for app state and UI data sharing. You still expose it as read-only observable in services to protect writes.

```ts
private readonly _count = new BehaviorSubject<number>(0);
readonly count$ = this._count.asObservable();

increment(): void { this._count.next(this._count.value + 1); }
```

---

## How do you perform error handling in Observables?
You can handle errors in `subscribe` callback or inside the pipeline using `catchError`. Pipeline handling is usually better because it keeps logic composable and reusable. You can recover by returning fallback values or rethrowing wrapped errors. `retry` and `retryWhen` are useful for transient failures. Always consider user messaging and logging, not only technical recovery.

```ts
this.http.get('/api/items').pipe(
  retry(1),
  catchError(() => of([]))
).subscribe(items => this.items = items);
```

---

## What are the utility functions/operators provided by RxJS?
RxJS provides creation, transformation, filtering, combination, and error-handling utilities. Frequently used operators include `map`, `filter`, `switchMap`, `mergeMap`, `debounceTime`, and `distinctUntilChanged`. For combining streams, use `combineLatest`, `forkJoin`, `zip`, and `withLatestFrom`. For lifecycle and cleanup, operators like `takeUntil`, `finalize`, and `shareReplay` are common. Good operator choice directly affects readability, performance, and correctness.

```ts
search$.pipe(
  debounceTime(300),
  distinctUntilChanged(),
  switchMap(q => this.http.get(`/api?q=${q}`))
);
```

---

## What is Reactive Programming and how does it relate to Angular?
Reactive programming models data and events as streams that change over time. Instead of imperative step-by-step flow, you declare how outputs react to input changes. Angular embraces this with RxJS, reactive forms, and async pipes. This style simplifies complex async behavior like live search, polling, and chained API calls. It also improves composability and testability of data flows.

```ts
this.results$ = this.form.valueChanges.pipe(
  debounceTime(250),
  switchMap(v => this.api.search(v.term))
);
```

---

## What is the difference between declarations, providers, and imports in NgModule?
`declarations` lists components, directives, and pipes that belong to the module. `providers` registers services in the dependency injection system. `imports` brings in exported functionality from other modules. Mixing these incorrectly often causes compile or runtime DI errors. A clean module setup makes features easier to compose and test.

```ts
@NgModule({
  declarations: [ListComponent, HighlightDirective],
  imports: [CommonModule, FormsModule],
  providers: [ListService]
})
export class ListModule {}
```

---

## Explain the difference between constructor and ngOnInit. Why use ngOnInit if a constructor already exists?
The constructor is for dependency injection and basic class initialization. `ngOnInit` is a lifecycle hook called by Angular after input bindings are set. Logic that depends on bound inputs or framework context should go in `ngOnInit`, not constructor. This separation improves clarity and avoids initialization timing bugs. Keep constructors lightweight and side-effect free when possible.

```ts
constructor(private api: ApiService) {}

ngOnInit(): void {
  this.loadData();
}
```

---

## What are the lifecycle hooks for components and directives?
Angular lifecycle hooks are callback methods invoked at key creation, update, and destruction stages. Common hooks include `ngOnChanges`, `ngOnInit`, `ngDoCheck`, `ngAfterContentInit`, `ngAfterViewInit`, and `ngOnDestroy`. They let you initialize data, react to input changes, and clean up resources. Not all hooks are needed in every component. Correct hook choice avoids timing issues and memory leaks.

```ts
export class DemoComponent implements OnInit, OnDestroy {
  ngOnInit(): void { /* init */ }
  ngOnDestroy(): void { /* cleanup */ }
}
```

---

## How do you categorize data binding types?
Angular has four common binding categories. Interpolation and property binding are one-way from component to view. Event binding is one-way from view to component. Two-way binding combines property and event binding, commonly via `[(ngModel)]`. Choosing the right type keeps templates explicit and predictable.

```html
<p>{{ name }}</p>
<input [value]="name" (input)="name = $any($event.target).value" />
<input [(ngModel)]="name" />
```

---

## What happens if you use a `script` tag inside an Angular template?
Angular treats template HTML as declarative view markup and does not execute script tags there. This is a security-focused behavior to reduce script injection risks. Script tags inserted through bindings are sanitized or ignored depending on context. You should place application scripts in build assets, not inline templates. For dynamic logic, use component code and bindings instead.

```html
<!-- Not executed as application script in Angular templates -->
<div [innerHTML]="'<script>alert(1)</script>'"></div>
```

---

## How do you choose between an inline and external template file?
Inline templates are convenient for very small, simple components. External templates scale better for readability, tooling support, and collaboration. Large templates become hard to maintain if embedded in TypeScript strings. External files also make diff reviews and HTML formatting easier. As a rule, use external templates unless the markup is tiny.

```ts
@Component({
  selector: 'app-inline',
  template: '<p>Small template</p>'
})
export class InlineComponent {}
```

---

## How would you run unit tests in Angular?
Angular unit tests are typically run with the Angular CLI. The common command is `ng test`, which uses Karma + Jasmine by default in many projects. Tests can run in watch mode during development or once in CI. You should mock dependencies and isolate component/service behavior. Good unit tests are fast, deterministic, and focused on one behavior at a time.

```ts
it('should create component', () => {
  const fixture = TestBed.createComponent(AppComponent);
  expect(fixture.componentInstance).toBeTruthy();
});
```

---

## What is TestBed?
TestBed is Angular’s primary utility for configuring and creating test modules. It simulates Angular runtime wiring for components, directives, pipes, and services. You define declarations, providers, and imports needed by the unit under test. It can create fixtures that expose component instance and rendered DOM. TestBed is essential for realistic Angular unit tests.

```ts
beforeEach(() => {
  TestBed.configureTestingModule({
    declarations: [LoginComponent],
    providers: [AuthService]
  });
});
```

---

## Why would you use a spy in a test?
A spy lets you observe function calls without using the real implementation. It helps isolate the unit under test from expensive or external dependencies. You can control returned values and assert invocation arguments. In Angular tests, spies are common for services, router navigation, and HTTP methods. This improves test reliability and speed.

```ts
const authSpy = jasmine.createSpyObj('AuthService', ['login']);
authSpy.login.and.returnValue(of(true));
expect(authSpy.login).not.toHaveBeenCalled();
```

---

## What does detectChanges do in Angular Jasmine tests?
`fixture.detectChanges()` runs Angular change detection for the test fixture. It applies bindings, updates the DOM, and triggers lifecycle hooks for initial render. Without it, template values may not reflect component state changes. Call it after state updates to assert final UI output. It is one of the most common causes of confusion in Angular tests.

```ts
component.title = 'New Title';
fixture.detectChanges();
expect(fixture.nativeElement.textContent).toContain('New Title');
```

---

## How do you create an application to use SCSS?
You can create a new Angular project configured for SCSS via CLI options. Use `--style=scss` so generated components use `.scss` files by default. In existing projects, update `angular.json` and rename styles accordingly. SCSS supports variables, mixins, and nesting for better style maintainability. Keep nesting shallow to avoid overly specific selectors.

```ts
// shell command
// ng new my-app --style=scss

// angular.json
// "schematics": { "@schematics/angular:component": { "style": "scss" } }
```

---

## How do you bundle an Angular app for production?
Use `ng build --configuration production` to produce optimized output. Production builds enable minification, dead code elimination, and build-time optimizations. Angular CLI also handles hashing filenames for caching strategies. You then deploy files from `dist/` to your hosting platform. Always validate bundle size and performance after release builds.

```ts
// shell command
// ng build --configuration production

// output path example: dist/my-app/browser
```

---

## How do you set headers for every request in Angular?
The standard approach is an `HttpInterceptor`. Interceptors can clone each request and append headers globally. This avoids repeating header setup in every service method. It is commonly used for auth tokens, language headers, and correlation IDs. Register the interceptor once in providers.

```ts
intercept(req: HttpRequest<unknown>, next: HttpHandler): Observable<HttpEvent<unknown>> {
  const authReq = req.clone({ setHeaders: { Authorization: 'Bearer token' } });
  return next.handle(authReq);
}
```

---

## How do you perform error handling for HttpClient?
Use RxJS operators such as `catchError` in service methods. Map backend errors to user-friendly messages or domain-specific errors. Centralize repeated logic in interceptors when appropriate. In UI, show fallback state and allow retry where meaningful. Avoid swallowing errors silently because observability matters in production.

```ts
getUsers(): Observable<User[]> {
  return this.http.get<User[]>('/api/users').pipe(
    catchError(err => throwError(() => new Error('Failed to load users')))
  );
}
```

---

## Could I use jQuery with Angular?
Technically yes, but it is generally discouraged. jQuery manipulates DOM imperatively, which can conflict with Angular’s rendering and change detection model. This often makes code harder to test and maintain. Prefer Angular templates, directives, Renderer2, and CDK utilities for UI behavior. If legacy integration is unavoidable, isolate jQuery usage behind wrappers.

```ts
ngAfterViewInit(): void {
  // Legacy-only example; avoid in modern Angular where possible
  // ($(this.el.nativeElement) as any).modal();
}
```

---

## What is Redux and how does it relate to an Angular app?
Redux is a predictable state management pattern based on single source of truth and immutable updates. In Angular, similar concepts are commonly implemented with NgRx. Actions describe events, reducers compute next state, and selectors read state for views. This is useful in large apps with complex shared state and debugging needs. For small apps, service-based state may be simpler.

```ts
export const increment = createAction('[Counter] Increment');
export const counterReducer = createReducer(0, on(increment, s => s + 1));
```

---

## What are dynamic components?
Dynamic components are created at runtime rather than declared directly in template HTML. They are useful for dialogs, plugin-like UIs, CMS blocks, and highly configurable layouts. In modern Angular, you typically use `ViewContainerRef.createComponent`. This allows passing inputs and subscribing to outputs programmatically. Remember to destroy dynamic refs when no longer needed.

```ts
const ref = this.vcr.createComponent(AlertComponent);
ref.instance.message = 'Saved successfully';
```

---

## What are Custom Elements in Angular, how do they work internally, and do they need bootstrapping?
Angular custom elements package components as standard web components. Internally, Angular maps component lifecycle and change detection to custom element callbacks. This lets non-Angular apps use Angular-built widgets via native HTML tags. You usually register elements with `createCustomElement` and `customElements.define`. They do not use normal Angular app bootstrapping in the same way as SPA roots.

```ts
const el = createCustomElement(WidgetComponent, { injector });
customElements.define('app-widget', el);
```

---

## What are the mapping rules between an Angular component and a custom element?
Component `@Input()` properties map to element attributes/properties. Outputs map to custom DOM events emitted from the element. Naming conventions often convert camelCase inputs to dash-case attributes. The component selector is not required as the custom element name is defined separately. Lifecycle hooks still run inside Angular context when element is connected.

```ts
@Component({ template: '' })
export class CardElementComponent {
  @Input() title = '';
  @Output() closed = new EventEmitter<void>();
}
```

---

## How can you run AngularJS and Angular side by side (ngUpgrade)?
Use the `@angular/upgrade` package to create a hybrid application. It allows AngularJS and Angular components/services to interoperate during migration. You typically bootstrap Angular and then upgrade/downgrade selected pieces incrementally. This reduces rewrite risk for large legacy systems. Migration can happen feature by feature instead of big-bang replacement.

```ts
platformBrowserDynamic().bootstrapModule(AppModule).then(ref => {
  const upgrade = ref.injector.get(UpgradeModule);
  upgrade.bootstrap(document.body, ['legacyApp']);
});
```

---

## Is there an equivalent to $scope.emit() or $scope.broadcast() in Angular?
Angular does not use `$scope` event propagation patterns from AngularJS. Instead, communication is done through `@Input/@Output`, shared services with RxJS subjects, or global state stores. For parent-child, outputs are preferred for explicit event flow. For distant components, a service event bus pattern is common. This results in clearer, testable communication than implicit scope events.

```ts
@Injectable({ providedIn: 'root' })
export class EventsService {
  private readonly _events = new Subject<string>();
  readonly events$ = this._events.asObservable();
  emit(name: string): void { this._events.next(name); }
}
```

---

## How would you control the size of an element on window resize in a component?
You can listen to resize events and update component state, then bind dimensions in template. A common approach is `@HostListener('window:resize')`. For performance, debounce rapid resize streams when doing heavier calculations. Access element dimensions via `ElementRef` or `ResizeObserver` when needed. Keep direct DOM access minimal and test behavior with mocked resize events.

```ts
@HostListener('window:resize')
onResize(): void {
  this.width = window.innerWidth;
}
```

---

## What is Zone/NgZone in Angular, and when would you use it?
Zone.js patches async APIs so Angular knows when to run change detection. `NgZone` gives control over whether code runs inside or outside Angular’s zone. Running expensive listeners outside Angular can reduce unnecessary checks. When UI updates are needed, re-enter the zone with `ngZone.run`. This is useful for performance tuning around third-party libraries or high-frequency events.

```ts
this.ngZone.runOutsideAngular(() => {
  window.addEventListener('scroll', () => {
    this.ngZone.run(() => this.scrolled = true);
  });
});
```

---

## What is the Angular equivalent of an AngularJS $watch?
Angular does not expose `$watch` in the same style as AngularJS. Equivalent behavior usually comes from bindings, lifecycle hooks like `ngOnChanges`, and RxJS streams. For forms, `valueChanges` is a common watch-like pattern. For custom mutable structures, you can use `KeyValueDiffers` or manual comparisons in `ngDoCheck`. Prefer explicit reactive flows over generic watchers.

```ts
ngOnChanges(changes: SimpleChanges): void {
  if (changes['user']) {
    this.loadUserDetails();
  }
}
```

---

## Why would you use renderer methods instead of native element methods?
Renderer2 abstracts DOM operations to keep code platform-safe and secure. Direct `nativeElement` manipulation can break server-side rendering or web worker scenarios. Renderer methods also align better with Angular’s rendering model. They can reduce security risks from unsafe direct DOM operations. Use native APIs only when necessary and controlled.

```ts
constructor(private renderer: Renderer2, private el: ElementRef) {}

ngAfterViewInit(): void {
  this.renderer.addClass(this.el.nativeElement, 'active');
}
```

---

## How would you insert an embedded view from a prepared TemplateRef?
Inject `ViewContainerRef` and call `createEmbeddedView` with a `TemplateRef`. This lets you render reusable template fragments dynamically. You can also provide a context object to pass local variables into the template. It is common in structural directives and advanced UI composition. Remember to clear container when replacing views.

```ts
@ViewChild('tpl') tpl!: TemplateRef<unknown>;

show(): void {
  this.vcr.clear();
  this.vcr.createEmbeddedView(this.tpl);
}
```

---

## Name and explain Angular module loading strategies.
The two main strategies are eager loading and lazy loading. Eager modules are loaded at startup, so navigation is immediate but initial bundle is larger. Lazy modules are loaded only when route is visited, reducing initial load time. Preloading strategies can load lazy modules in background after app starts. Strategy choice depends on app size, traffic patterns, and UX priorities.

```ts
RouterModule.forRoot(routes, {
  preloadingStrategy: PreloadAllModules
})
```

---

## When would you use eager loading?
Use eager loading for core features needed immediately at startup. It is suitable for small modules with high navigation frequency. Eager loading avoids first-hit delay when entering that feature. It can simplify routing in smaller applications. Do not overuse it in large apps because startup bundle can become heavy.

```ts
const routes: Routes = [
  { path: 'dashboard', component: DashboardComponent }
];
```

---

## What is lazy loading in Angular, why use it, and when is a lazy-loaded module loaded?
Lazy loading defers module code download until user navigates to a route. This reduces initial bundle size and speeds first content load. It is especially valuable for large enterprise apps with many feature areas. A lazy module loads the first time its route is matched, unless preloading is enabled. After loading, navigation to that module is usually much faster.

```ts
const routes: Routes = [
  { path: 'admin', loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule) }
];
```

---

## What is the need for SystemJS in Angular?
SystemJS was historically used as a dynamic module loader in early Angular setups. It helped load ES modules in browsers before modern bundlers became standard. Today, Angular CLI projects generally rely on webpack or esbuild-based tooling instead. SystemJS may still appear in legacy apps or demos. In modern production Angular, it is rarely required.

```ts
// Legacy SystemJS config style
System.config({
  map: { app: 'app' }
});
```

---

## What are key differences between SystemJS and webpack?
SystemJS is mainly a runtime module loader, while webpack is a build-time bundler and optimizer. Webpack can tree-shake, split chunks, and optimize assets for production. SystemJS gives flexible runtime loading but fewer advanced optimizations by default. Angular CLI deeply integrates with bundlers, not SystemJS, in modern workflows. For production-grade Angular apps, webpack-like tooling is preferred.

```ts
// webpack-style lazy import
import('./feature/feature.module').then(m => m.FeatureModule);
```

---

## How would you extract webpack config from an Angular CLI project?
Angular CLI hides webpack internals to keep configuration simple and consistent. Historically, people used tools like `ngx-build-plus` or custom builders to extend config. In newer Angular versions, the default builder may rely on esbuild-based pipelines depending on setup. Direct full config extraction is not the normal path and can be brittle. Prefer official extension points or custom builders when customization is required.

```ts
// angular.json (conceptual)
// "builder": "ngx-build-plus:browser"
// allows extending underlying bundler configuration
```

---

## Why do we need a compilation process in Angular?
Compilation translates templates and decorators into efficient JavaScript instructions. It catches template/type errors early during build. The compiler also performs optimizations and metadata processing for dependency injection. This process improves runtime performance and startup behavior. Without compilation, Angular would rely more heavily on runtime reflection and be slower.

```ts
@Component({
  selector: 'app-item',
  template: '<p>{{ item.name }}</p>'
})
export class ItemComponent { item = { name: 'Book' }; }
```

---

## What does a just-in-time (JIT) compiler do?
JIT compiles Angular templates in the browser at runtime. It is convenient during development because rebuilds are flexible and debug-friendly. However, it adds runtime compilation cost and larger shipped metadata. That is why production builds usually avoid JIT. JIT is mostly used for local development workflows.

```ts
platformBrowserDynamic().bootstrapModule(AppModule);
```

---

## What is AOT, what are its advantages, and how is it different from JIT?
AOT compiles templates at build time, before code reaches the browser. Compared to JIT, it produces smaller bundles and faster startup. It also catches many template errors earlier in CI pipelines. JIT compiles at runtime and is typically slower for initial load. For production Angular apps, AOT is the standard choice.

```ts
// shell command
// ng build --configuration production
// production build enables AOT by default in modern Angular
```

---

## What are ways to control AOT compilation?
You control AOT through Angular CLI build configurations. In modern projects, production config enables AOT by default. You can explicitly pass `--aot` or `--no-aot` for specific builds. In `angular.json`, configurations define optimization and compilation behavior per environment. This allows different settings for development, staging, and production.

```ts
// shell commands
// ng build --aot
// ng serve --no-aot
```

---

## What is Angular Ivy?
Ivy is Angular’s modern compilation and rendering pipeline introduced as the default engine. It improves build speed, debugging experience, and bundle output. Ivy also enables better tree-shaking and more granular compilation. It supports advanced features like improved type checking and simpler generated code. Most current Angular versions run on Ivy by default.

```ts
// Ivy is internal by default; no special component syntax is required
@Component({ selector: 'app-root', template: '<p>Ivy app</p>' })
export class AppComponent {}
```

---

## What is Ivy Renderer?
Ivy Renderer is the runtime part that executes instructions generated by Ivy compiler. Instead of large factory metadata patterns from older engine, it uses lean instruction-based output. This helps reduce framework overhead and improve tree-shakability. It also makes incremental builds and debugging friendlier. From a developer perspective, usage is transparent because Angular handles it internally.

```ts
// Conceptual only: Ivy compiles template to instructions behind the scenes
@Component({ template: '<span>{{ label }}</span>' })
export class LabelComponent { label = 'Hi'; }
```

---

## How would you compare View Engine vs Ivy?
View Engine is Angular’s older compiler/renderer architecture. Ivy is newer, faster, and usually generates smaller output with better tree-shaking. Ivy improves template type checking and local compilation behavior. It also reduced complexity around library compatibility over time. Today, Ivy is the recommended and default path for modern Angular development.

```ts
// No code changes needed by app developers when moving from View Engine to Ivy
@NgModule({ declarations: [AppComponent] })
export class AppModule {}
```

---

## What is the Locality principle in Ivy?
Locality means a component can be compiled mostly from its own metadata without global program knowledge. This enables faster incremental builds because fewer files need recompilation for local changes. It improves developer feedback loops in large projects. Locality also helps tooling and language service performance. In practice, edits in one component have smaller compile impact.

```ts
@Component({
  selector: 'app-local',
  template: '{{ value }}'
})
export class LocalComponent { value = 1; }
```

---

## How does Ivy affect rebuild time?
Ivy generally reduces rebuild times through more granular compilation and locality. Incremental changes recompile fewer affected units compared with older architecture. This improves `ng serve` experience and developer productivity. The impact is most visible in medium-to-large apps. Faster rebuilds mean quicker validation and shorter iteration cycles.

```ts
// Typical workflow benefiting from Ivy rebuild improvements
// ng serve
// edit one component -> faster recompilation feedback
```

---

## What is Incremental DOM, and how is it different from Virtual DOM?
Virtual DOM builds in-memory tree representations and diffs them before patching real DOM. Incremental DOM applies fine-grained updates directly while traversing templates, reducing intermediate allocations. Angular’s Ivy instruction model aligns with an incremental update style. This can reduce memory pressure in complex UIs. Both approaches aim to minimize expensive real DOM operations, but implementation tradeoffs differ.

```ts
// Conceptual Angular template update
@Component({ template: '<p>{{ count }}</p>' })
export class CounterComponent { count = 0; }
```

---

## Why does Incremental DOM have a low memory footprint and support tree shaking?
Incremental update models avoid creating large temporary virtual trees on each render pass. Fewer intermediate objects typically means lower memory churn and less GC pressure. Ivy also emits instruction-level code that can be tree-shaken when features are unused. This keeps shipped bundles leaner in many scenarios. Together, these characteristics help runtime and payload efficiency.

```ts
// Build optimization context
// ng build --configuration production
// enables optimizations and tree-shaking
```

---

## Why did the Google team choose Incremental DOM instead of Virtual DOM?
The main goals were performance predictability, memory efficiency, and better integration with Angular compilation. Incremental update strategy works well with generated template instructions. It avoids keeping large parallel trees in memory for diffing. This can be beneficial on lower-end devices and complex enterprise screens. The choice reflects framework-level tradeoffs rather than a universal rule for all UI libraries.

```ts
@Component({
  template: '<ul><li *ngFor="let i of items">{{ i }}</li></ul>'
})
export class ListComponent { items = [1, 2, 3]; }
```

---

## Explain the purpose of Service Workers in Angular.
Service workers enable offline support, caching strategies, and background update behavior for PWAs. Angular provides built-in integration through `@angular/service-worker`. They can cache static assets and selected API responses for faster repeat visits. Service workers also help reliability on flaky networks. You should design caching carefully to avoid stale data issues.

```ts
// shell command
// ng add @angular/pwa

// enables service worker in production builds
```

---

## What is Angular Universal?
Angular Universal is Angular’s server-side rendering (SSR) solution. It renders HTML on the server before sending it to the browser. This improves first contentful paint, SEO, and social sharing previews. After initial render, app hydrates and continues as a client-side SPA. Universal is useful for content-heavy or performance-sensitive public pages.

```ts
// shell command
// ng add @nguniversal/express-engine
```

---

## What is Protractor?
Protractor is an end-to-end testing framework historically built for Angular apps on top of WebDriverJS. It offered Angular-aware synchronization in earlier ecosystem stages. However, it has been deprecated and is no longer the recommended choice. Modern alternatives include Cypress, Playwright, and WebdriverIO. In interviews, mention Protractor mainly as legacy context.

```ts
// Legacy Protractor example
// element(by.css('button.save')).click();
```

---

## What is Bazel, and why would you use it for Angular builds?
Bazel is a build system focused on speed, reproducibility, and scalability for large monorepos. It uses fine-grained dependency graphs and caching to avoid unnecessary rebuilds. Angular tooling has had Bazel integrations for specific enterprise scenarios. Teams choose it when they need consistent builds across huge multi-language codebases. For typical Angular apps, CLI defaults are usually sufficient.

```ts
// Conceptual Bazel target
// bazel build //apps/web:prod
```

---

## What is the use of Codelyzer?
Codelyzer is a static analysis tool that enforced Angular style and best practices in older TSLint-based setups. It helped catch anti-patterns and maintain consistency across teams. Since TSLint is deprecated, many projects migrated to ESLint with Angular ESLint plugins. Still, Codelyzer appears in legacy codebases and interview questions. The core idea is automated linting for quality gates.

```ts
// Modern equivalent stack
// @angular-eslint + eslint rules
```

---

## Name some security best practices in Angular.
Rely on Angular’s built-in sanitization and avoid bypassing it unless absolutely necessary. Never trust user input; validate on both client and server. Use HttpOnly, Secure, SameSite cookies for sensitive tokens where applicable, and apply CSP headers. Keep dependencies updated and audit packages regularly. Also enforce route guards, output encoding, and least-privilege API design.

```ts
// Safe binding patterns
// <div>{{ userInput }}</div>
// <div [innerHTML]="trustedHtml"></div> // only when content is trusted and sanitized
```

---

## What are pros/cons (especially performance-wise) of using local storage to replace cookies?
Local storage offers larger capacity and avoids sending data with every HTTP request, which can reduce request overhead. However, it is accessible via JavaScript, so XSS risk is higher for sensitive data. Cookies can be HttpOnly and automatically included by browser in requests, which is useful for server sessions. Local storage is synchronous and can block main thread for heavy operations. Use local storage for non-sensitive client state, not as a direct cookie replacement for secure auth sessions.

```ts
localStorage.setItem('theme', 'dark');
const theme = localStorage.getItem('theme');
```

---

## How do you detect a route change in Angular?
Subscribe to `Router.events` and filter for navigation event types like `NavigationEnd`. This lets you run logic after route transitions complete. Common use cases include analytics, scroll handling, and context-based UI updates. Always unsubscribe when needed, or use operators tied to component lifecycle. Route change hooks should stay lightweight to avoid navigation lag.

```ts
this.router.events.pipe(
  filter(e => e instanceof NavigationEnd)
).subscribe(() => console.log('route changed'));
```

---

## When do you use query parameters versus matrix parameters in URL?
Query parameters are key-value pairs after `?` and are common for filtering, paging, and optional state. Matrix parameters attach to individual path segments using `;`, useful for segment-specific metadata. Query params are widely understood across tools and backend systems. Matrix params are less common but supported by Angular Router. Choose based on API style, readability, and interoperability needs.

```ts
// Query: /products?page=2&sort=asc
this.router.navigate(['/products'], { queryParams: { page: 2, sort: 'asc' } });

// Matrix: /products;page=2;sort=asc
```

---

## Why does Angular use URL segments?
URL segments map naturally to hierarchical routes and nested component structures. This makes routing predictable and composable for child routes and route parameters. Segment-based parsing also supports guards, resolvers, and lazy-loaded boundaries cleanly. It helps build meaningful, shareable URLs that reflect application state. Overall, segment modeling aligns router behavior with web navigation conventions.

```ts
const routes: Routes = [
  { path: 'users/:id/details', component: UserDetailsComponent }
];
```

---

## Angular 9: What are some new features?
Angular 9 introduced Ivy as the default compiler and renderer, which was the biggest change. It also improved template type checking and build output diagnostics. Differential loading behavior and build optimizations became more practical for production apps. The update improved testing and migration tooling through CLI schematics. Many teams saw better build performance and easier debugging after upgrade.

```ts
// Upgrade command example
// ng update @angular/core @angular/cli
```

---

## Angular 9: Explain improvements in tree-shaking.
With Ivy, generated code became more localized and instruction-based, which helps bundlers remove unused pieces more effectively. Better static analysis of metadata reduced retained dead code. This improved final bundle size in many real projects. Smaller bundles typically improve initial load and parse times. Tree-shaking gains are strongest when libraries are authored with modern Angular packaging practices.

```ts
// Build analyzer workflow
// ng build --configuration production
// npx source-map-explorer dist/**/main*.js
```

---

## Angular 8: What are some changes in the Location module?
Angular 8 included enhancements around router and location interoperability, especially for improved navigation behavior. It also aligned with broader platform updates and differential loading era tooling. While not as headline-grabbing as Ivy, location-related APIs remained important for URL manipulation and history control. Teams commonly used `Location` service for back navigation and path checks in components. Interviewers usually expect understanding of practical usage rather than memorizing minor version internals.

```ts
constructor(private location: Location) {}

goBack(): void {
  this.location.back();
}
```

---
