# 20 Angular Interview Trap / Gotcha Questions
### Sorted from simple → advanced, with reasoning, correct answers, and commented code

---

## 1. What does `*ngIf` actually do to the DOM (vs `[hidden]`)?

**The trap:** People say "it hides the element," confusing it with CSS `display: none`.

**Answer:** `*ngIf` **adds/removes** the element from the DOM entirely (destroys and recreates the component/view). `[hidden]` or `[style.display]` just toggles CSS visibility — the element stays in the DOM and keeps its state.

```html
<!-- ngIf: element + component instance are destroyed when condition is false.
     Any local state (e.g. form input) is lost, ngOnDestroy fires. -->
<app-widget *ngIf="showWidget"></app-widget>

<!-- hidden: element stays in DOM, just CSS display:none. State is preserved. -->
<app-widget [hidden]="!showWidget"></app-widget>
```

**Why it matters:** Frequent toggling with `*ngIf` re-runs the whole lifecycle (constructor → ngOnInit) each time, which is expensive. `[hidden]` is cheaper for frequent toggles but keeps inactive components running (timers, subscriptions) in the background — a memory/CPU trade-off interviewers love to probe.

---

## 2. Why does interpolation `{{ }}` always convert to a string?

**The trap:** Candidates think `{{ }}` can bind objects/functions directly like property binding.

**Answer:** Interpolation is syntactic sugar over `textContent` (or attribute) binding, so Angular calls `.toString()` on the expression result.

```html
<!-- If user = { name: 'Ann' }, this prints "[object Object]" -->
<p>{{ user }}</p>

<!-- Correct: interpolate a primitive value -->
<p>{{ user.name }}</p>
```

**Concept:** Interpolation ≠ property binding. `[prop]="expr"` passes the actual JS value/reference; `{{ expr }}` always coerces to string.

---

## 3. Difference between `ng-template`, `ng-container`, and `ng-content`

**The trap:** Interviewers ask this to see if you actually understand structural directives vs projection, not just memorized definitions.

**Answer:**
- `ng-template`: defines a **template block** that is not rendered unless explicitly instantiated (e.g., by `*ngIf`, `*ngFor`, or `TemplateRef`).
- `ng-container`: a **non-rendering grouping element** — lets you apply a structural directive without adding an extra DOM node (no `<div>` wrapper).
- `ng-content`: used for **content projection** — inserts content passed from a parent component into a child's template.

```html
<!-- ng-container: no wrapping element in final DOM, just groups two structural directives -->
<ng-container *ngIf="isLoggedIn">
  <span *ngFor="let n of notifications">{{ n }}</span>
</ng-container>

<!-- ng-template: nothing renders here unless referenced elsewhere -->
<ng-template #elseBlock>
  <p>Please log in</p>
</ng-template>

<!-- ng-content inside a child component's template: -->
<!-- <div class="card"><ng-content></ng-content></div> -->
<!-- Parent usage: <app-card><h1>Injected content</h1></app-card> -->
```

---

## 4. Do lifecycle hooks fire in a predictable, fixed order?

**The trap:** People forget the exact order or think `ngOnInit` runs before the constructor.

**Answer:** Order is: `constructor` → `ngOnChanges` (only if there are `@Input()`s) → `ngOnInit` → `ngDoCheck` → `ngAfterContentInit` → `ngAfterContentChecked` → `ngAfterViewInit` → `ngAfterViewChecked` → ... → `ngOnDestroy`.

```typescript
export class ChildComponent implements OnChanges, OnInit, OnDestroy {
  @Input() value!: string;

  constructor() {
    // DI happens here. @Input() properties are NOT yet set!
    console.log(this.value); // undefined
  }

  ngOnChanges(changes: SimpleChanges): void {
    // Fires BEFORE ngOnInit, and again on every input change afterward.
    console.log(changes['value'].currentValue);
  }

  ngOnInit(): void {
    // Runs once, after the first ngOnChanges. Safe place to read @Input()s.
    console.log(this.value);
  }

  ngOnDestroy(): void {
    // Cleanup: unsubscribe, clear timers, detach listeners.
  }
}
```

**Concept:** The constructor is plain TypeScript/JS — Angular hasn't bound inputs yet. Never rely on `@Input()` values inside the constructor.

---

## 5. Why does mutating an array/object in place NOT trigger change detection with `OnPush`?

**The trap:** The classic Angular gotcha — "I pushed a new item but the view didn't update!"

**Answer:** `ChangeDetectionStrategy.OnPush` checks a component only when: (a) an `@Input()` reference changes, (b) an event originates from the component or its children, or (c) an observable bound via the `async` pipe emits. Mutating an array in place keeps the **same reference**, so Angular's reference check (`===`) sees no change.

```typescript
@Component({
  selector: 'app-list',
  changeDetection: ChangeDetectionStrategy.OnPush,
  template: `<li *ngFor="let item of items">{{ item }}</li>`
})
export class ListComponent {
  @Input() items: string[] = [];

  addItemWrong(newItem: string) {
    // BAD: same array reference -> OnPush won't detect the change
    this.items.push(newItem);
  }

  addItemRight(newItem: string) {
    // GOOD: creates a brand-new array reference -> triggers change detection
    this.items = [...this.items, newItem];
  }
}
```

**Concept tested:** Immutability is not a style preference in Angular — it's how `OnPush` decides whether to re-check a component subtree. This ties directly into interviewers' favorite follow-up: "How does Angular's default change detection differ from `OnPush`?" (Default walks the *entire* component tree on every event; `OnPush` skips subtrees whose inputs didn't change reference.)

---

## 6. Why do two-way bindings on `[(ngModel)]` sometimes desync from the model?

**The trap:** People assume `[(ngModel)]` is magic and always in sync.

**Answer:** `[(ngModel)]` is just sugar for `[ngModel]="value" (ngModelChange)="value = $event"`. If change detection doesn't run (e.g., inside a `setTimeout` outside Angular's zone, or with `OnPush` without triggering a check), the displayed value can lag behind the actual property.

```typescript
// Banana-in-a-box syntax expands to this:
// <input [ngModel]="name" (ngModelChange)="name = $event">

updateOutsideAngular() {
  // If this component is OnPush and this runs outside a triggering event,
  // the bound input might not visually update immediately.
  this.name = 'Changed programmatically';
}
```

**Concept:** Understanding that two-way binding is syntactic sugar (not a special mechanism) is exactly the kind of "gotcha" that separates memorizers from people who understand Angular's binding model.

---

## 7. Why does `subscribe()` sometimes run your callback multiple times unexpectedly?

**The trap:** Classic RxJS/Angular trap — HTTP calls firing twice, or template subscriptions multiplying.

**Answer:** Observables are **lazy and unicast by default** — every `subscribe()` call re-executes the producer. Also, using the `async` pipe *and* manually subscribing to the same observable in a template both create separate subscriptions/executions.

```typescript
// BAD: two separate HTTP requests are fired because http.get() returns
// a *cold* observable — each subscribe() re-triggers execution.
const data$ = this.http.get('/api/data');
data$.subscribe(res => console.log('sub1', res)); // fires request #1
data$.subscribe(res => console.log('sub2', res)); // fires request #2

// GOOD: share the single execution among multiple subscribers.
const shared$ = this.http.get('/api/data').pipe(
  shareReplay(1) // caches/replays the last emission to all subscribers
);
shared$.subscribe(res => console.log('sub1', res));
shared$.subscribe(res => console.log('sub2', res)); // reuses cached result, no 2nd request
```

**Concept:** Cold vs hot observables. HTTP requests via `HttpClient` are cold — think of `subscribe()` as "run this producer again," not "listen to an existing stream."

---

## 8. Why is `async` pipe usually preferred over manual `subscribe()` in components?

**The trap:** Interviewers want to see if you know about memory leaks, not just "it's cleaner."

**Answer:** The `async` pipe automatically **subscribes on init and unsubscribes on destroy**, preventing memory leaks. Manual subscriptions require you to remember to unsubscribe (usually in `ngOnDestroy`), which is a common source of leaks and duplicate work in real codebases.

```typescript
// BAD: manual subscription without cleanup -> memory leak,
// the callback keeps running even after the component is destroyed.
export class BadComponent implements OnInit {
  data: any;
  ngOnInit() {
    this.userService.getUser().subscribe(u => this.data = u);
  }
  // No ngOnDestroy -> subscription lives forever if the source never completes
}

// GOOD: template handles subscribe/unsubscribe automatically.
@Component({
  template: `<div *ngIf="user$ | async as user">{{ user.name }}</div>`
})
export class GoodComponent {
  user$ = this.userService.getUser(); // observable, not subscribed manually
}
```

**Concept:** "Who manages the subscription lifecycle?" is the real question — `async` pipe ties it to the component's own lifecycle automatically.

---

## 9. What's the actual difference between `Observable` and `Promise` (beyond "one can emit multiple values")?

**The trap:** Most candidates give the one-liner and stop, missing the deeper mechanics interviewers are probing for.

**Answer:** Key distinctions: <cite index="1-1">promises are executed immediately whereas observables are lazy, promises can't be cancelled whereas observables are cancellable, and promises handle a single value whereas observables can emit multiple values over time</cite>. Additionally, Observables have a rich operator library (`map`, `switchMap`, `debounceTime`, etc.) for composing async logic declaratively.

```typescript
// Promise: executes immediately upon creation, regardless of .then()
const promise = new Promise(resolve => {
  console.log('runs immediately'); // logs right away
  resolve(42);
});

// Observable: nothing happens until subscribe() is called
const observable = new Observable(subscriber => {
  console.log('runs only on subscribe'); // logs only when subscribed
  subscriber.next(42);
});
observable.subscribe(); // NOW the producer function runs

// Cancellation: only Observables support this natively
const sub = observable.subscribe();
sub.unsubscribe(); // stops the stream / cleans up resources
```

---

## 10. Why can injecting a service in the constructor sometimes give you a *different instance* than expected?

**The trap:** Candidates assume all services are automatically app-wide singletons.

**Answer:** Whether you get a singleton depends on **where the service is provided**. `providedIn: 'root'` gives a true app-wide singleton, but if a service is also listed in a component's `providers` array, Angular creates a **new instance scoped to that component's injector subtree**, shadowing the root one.

```typescript
@Injectable({ providedIn: 'root' }) // singleton across the whole app by default
export class CounterService {
  count = 0;
}

@Component({
  selector: 'app-child',
  providers: [CounterService] // <-- creates a NEW instance just for this component tree,
                               //     hiding the root singleton for this component and its children
  template: `...`
})
export class ChildComponent {
  constructor(private counter: CounterService) {
    // This 'counter' is NOT the same instance as in a sibling component
    // that injects CounterService without a local `providers` override.
  }
}
```

**Concept:** Angular's **hierarchical dependency injection** — injectors form a tree, and the nearest provider in the ancestor chain wins.

---

## 11. Why does injecting `HttpClient` (or any service) via the constructor sometimes throw `NullInjectorError`?

**The trap:** Candidates blame Angular being "buggy" instead of understanding module/provider wiring.

**Answer:** This error means the injector couldn't find a provider for that token anywhere up the injector tree — usually because the module providing it (e.g., `HttpClientModule`, or a `provideHttpClient()` call in standalone bootstrap) was never imported/registered.

```typescript
// Standalone app bootstrap (Angular 17+) — this is the modern trap:
// Forgetting provideHttpClient() causes NullInjectorError: No provider for HttpClient!
bootstrapApplication(AppComponent, {
  providers: [
    provideRouter(routes),
    provideHttpClient(), // <-- REQUIRED, easy to forget in standalone apps
  ]
});
```

**Concept:** DI errors are almost always a *registration* problem, not a "the framework is broken" problem — trace the injector tree back to the root.

---

## 12. Why does an `@Input()` value appear as `undefined` inside `ngOnInit` sometimes, even though it was passed from the parent?

**The trap:** Deceptively subtle — often caused by structural directive timing or async parent data.

**Answer:** If the parent itself hasn't received the data yet (e.g., it's waiting on an async call), Angular renders the child with whatever value existed *at that render pass* — often `undefined`. Because `ngOnInit` runs only once, it captures a stale snapshot. The fix is to react to `ngOnChanges` (which fires on every input update) instead of relying solely on `ngOnInit`.

```typescript
export class ChildComponent implements OnChanges {
  @Input() user?: User;

  ngOnChanges(changes: SimpleChanges): void {
    // Fires every time `user` changes reference — including the first time
    // it goes from undefined to a real object once the parent's async data arrives.
    if (changes['user'] && changes['user'].currentValue) {
      this.processUser(changes['user'].currentValue);
    }
  }

  private processUser(user: User) { /* ... */ }
}
```

---

## 13. Why does `*ngFor` sometimes destroy and rebuild every DOM row even when only one item changed?

**The trap:** Performance gotcha frequently asked at mid/senior level.

**Answer:** By default, `*ngFor` tracks items **by object identity**. If you replace the whole array (e.g., after an API refetch) with new object references — even if the *data* is logically the same — Angular can't tell which rows are "the same" and re-renders everything. The fix is `trackBy`.

```typescript
@Component({
  template: `
    <!-- Without trackBy: Angular compares objects by reference by default,
         so a new array of "equal" objects still means "destroy everything, recreate everything" -->
    <li *ngFor="let item of items">{{ item.name }}</li>

    <!-- With trackBy: Angular uses item.id to match old vs new rows,
         so only rows whose id actually changed get re-rendered/re-animated -->
    <li *ngFor="let item of items; trackBy: trackById">{{ item.name }}</li>
  `
})
export class ListComponent {
  items: Item[] = [];

  // Returning a stable identifier tells Angular's diffing algorithm
  // "this is the same logical row," preserving DOM nodes and component state.
  trackById(index: number, item: Item): number {
    return item.id;
  }
}
```

---

## 14. Why does calling a method directly inside a template (e.g., `{{ getTotal() }}`) hurt performance?

**The trap:** Looks harmless, but it's a very common senior-interview red flag to catch in code review.

**Answer:** Any function call in a template is re-invoked on **every** change detection cycle (which can fire dozens of times per user interaction). If `getTotal()` does real computation, you're redoing that work constantly, even when nothing relevant changed.

```typescript
// BAD: recalculated on every single change detection pass across the whole app
// template: <p>Total: {{ getTotal() }}</p>
getTotal(): number {
  return this.items.reduce((sum, i) => sum + i.price, 0); // expensive, repeated needlessly
}

// GOOD OPTION 1: use a pure pipe — Angular only recomputes when the *input reference* changes
@Pipe({ name: 'total', pure: true })
export class TotalPipe implements PipeTransform {
  transform(items: Item[]): number {
    return items.reduce((sum, i) => sum + i.price, 0);
  }
}
// template: <p>Total: {{ items | total }}</p>

// GOOD OPTION 2: precompute and store as a property, updated only when items actually change
recalculateTotal() {
  this.total = this.items.reduce((sum, i) => sum + i.price, 0);
}
```

**Concept:** Pure pipes are memoized against their input reference — a direct application of the immutability/`OnPush` mindset from question #5.

---

## 15. Why can two sibling components' services "leak" state into each other unexpectedly?

**The trap:** Often shows up as "why does resetting form A also reset form B?"

**Answer:** If a shared service is provided at a common ancestor (e.g., the root, or a shared parent module) instead of being scoped per-component, siblings receive the **same instance** and mutate shared state. This is the DI hierarchy trap from question #10, but flipped: sometimes you *don't* want a singleton.

```typescript
// If FormStateService is providedIn: 'root', every component that injects it
// shares one instance — good for truly global state, bad for "per-form" state.
@Injectable({ providedIn: 'root' })
export class FormStateService {
  draft: any = {};
}

// Fix: provide it locally on each form component so each gets its own instance,
// scoped to that component's injector subtree and destroyed when the component is.
@Component({
  selector: 'app-form-a',
  providers: [FormStateService], // isolates state per component instance
})
export class FormAComponent {}
```

---

## 16. Why does a route guard's `canActivate` sometimes let navigation through even when it looks like it "returned false"?

**The trap:** People forget guards can return Observables/Promises, and async timing bites them.

**Answer:** `canActivate` can return `boolean`, `UrlTree`, `Observable<boolean|UrlTree>`, or `Promise<...>`. If you return an Observable that **never completes** or resolves to a truthy-looking value by mistake, navigation proceeds unexpectedly. A common bug: forgetting to `map` an HTTP response into an actual boolean.

```typescript
export const authGuard: CanActivateFn = () => {
  const auth = inject(AuthService);

  // BAD: the raw HTTP response object is always "truthy" once it arrives,
  // regardless of the actual authentication status inside it.
  // return auth.checkSession(); // returns Observable<{ valid: boolean }>, always truthy object

  // GOOD: explicitly map the response into a real boolean/UrlTree
  return auth.checkSession().pipe(
    map(response => response.valid === true ? true : inject(Router).parseUrl('/login'))
  );
};
```

---

## 17. Why does `ChangeDetectorRef.detectChanges()` sometimes throw `ExpressionChangedAfterItHasBeenCheckedError`?

**The trap:** A very well-known but poorly-understood runtime error.

**Answer:** Angular runs change detection **twice in dev mode** to verify stability — if a bound value changes *during* the check cycle (e.g., in `ngAfterViewInit`, you set a property that affects the view), the second pass sees a different value than the first, and Angular throws to protect against inconsistent UI state.

```typescript
export class ParentComponent implements AfterViewInit {
  message = 'Initial';

  ngAfterViewInit(): void {
    // BAD: mutating a bound property after the view was already checked
    // in this change detection cycle triggers the error in dev mode.
    this.message = 'Updated'; // ExpressionChangedAfterItHasBeenCheckedError

    // GOOD OPTION 1: defer to the next cycle (macrotask)
    setTimeout(() => this.message = 'Updated');

    // GOOD OPTION 2: explicitly force a fresh check this same tick
    // this.message = 'Updated';
    // this.cdRef.detectChanges();
  }

  constructor(private cdRef: ChangeDetectorRef) {}
}
```

**Concept:** This error is a **development-mode safety net**, not a production bug indicator — it means "you mutated state during rendering," a violation of unidirectional data flow.

---

## 18. Why does a `Signal`-based computed value sometimes NOT update, even though a dependency Signal changed?

**The trap:** New (Angular 16+) API, and interviewers use it to check if you understand reactive dependency tracking, not just syntax.

**Answer:** `computed()` only re-evaluates if it **read** a signal synchronously during its last execution — dependencies are tracked automatically, but only for signals actually *called* (via their getter function) inside the computation. Conditionally-read signals (e.g., inside an `if` branch that wasn't taken) won't be tracked as dependencies until that branch actually executes.

```typescript
const showDiscount = signal(false);
const price = signal(100);
const discount = signal(10);

// This computed only reads `discount` when showDiscount() is true.
// If showDiscount is currently false, `discount` isn't tracked as a dependency yet —
// changing `discount` won't retrigger this computed until showDiscount flips to true
// and the computed actually executes that branch.
const finalPrice = computed(() => {
  if (showDiscount()) {
    return price() - discount();
  }
  return price();
});
```

**Concept:** Signals use **fine-grained, dynamic dependency tracking** based on what's actually read during execution — a fundamentally different (pull-based, synchronous) model compared to RxJS's push-based streams.

---

## 19. Why might switching from Zone.js change detection to `provideExperimentalZonelessChangeDetection()` silently break existing components?

**The trap:** Tests seniority — knowing that zoneless Angular is not a drop-in performance toggle.

**Answer:** Zone.js patches async APIs (`setTimeout`, DOM events, Promises) and automatically triggers change detection after them. Without Zone.js, Angular only re-renders when it's explicitly told to (via Signals, `markForCheck()`, or the `async` pipe). Components that mutate plain class properties directly (not Signals) and rely on Zone.js's "automatic" refresh will stop updating the view.

```typescript
// Works fine WITH Zone.js: setTimeout is patched, so Angular
// automatically re-checks the view after this callback runs.
setTimeout(() => {
  this.count++; // Zone.js triggers change detection -> view updates
}, 1000);

// In a ZONELESS app, the above silently fails to update the view,
// because nothing tells Angular to re-render. The fix is to use Signals,
// which notify Angular directly when read/write happens, independent of Zone.js:
count = signal(0);
setTimeout(() => {
  this.count.update(c => c + 1); // Signal write triggers reactivity directly, no Zone needed
}, 1000);
```

**Concept:** Zoneless Angular shifts change-detection triggering from "automatic instrumentation of async APIs" to "explicit reactive primitives" (Signals). Migrating requires auditing every place that relied on implicit Zone.js triggering.

---

## 20. Why can two components using `OnPush` and Signals still cause an infinite change detection loop?

**The trap:** The hardest one — combines OnPush, Signals, and effects, and is a real production bug pattern.

**Answer:** An `effect()` that both **reads** and **writes** the same signal (directly or transitively through a computed chain) can retrigger itself indefinitely, since writing a signal it depends on schedules the effect to run again.

```typescript
export class BuggyComponent {
  count = signal(0);
  doubled = computed(() => this.count() * 2);

  constructor() {
    // BAD: this effect reads `count` (via `doubled`, which depends on it)
    // and also writes to `count` — every write reschedules the effect,
    // which writes again, forever. Angular will eventually throw
    // "effect() cannot write to signals it reads" or loop until a guard trips.
    effect(() => {
      console.log(this.doubled());
      this.count.set(this.count() + 1); // re-triggers this same effect
    });
  }
}

// GOOD: separate the read-side effect (e.g., for logging/side effects)
// from the write, and gate the write behind an explicit user action
// or an untracked read so it doesn't re-subscribe the effect to itself.
export class FixedComponent {
  count = signal(0);
  doubled = computed(() => this.count() * 2);

  constructor() {
    effect(() => {
      console.log('doubled is now', this.doubled()); // read-only, no write back
    });
  }

  increment() {
    this.count.update(c => c + 1); // writes happen from explicit user actions, not inside the effect
  }
}
```

**Concept:** `effect()` in Angular Signals is meant for side effects that **react to** state, not ones that **mutate the state they depend on**. This is the Signals-era equivalent of the classic "infinite `ngDoCheck` loop" bug from Zone.js-based Angular.

---

## Quick reference: concept map

| # | Core concept being tested |
|---|---|
| 1–3 | Template syntax fundamentals (DOM structure vs projection) |
| 4 | Lifecycle hook ordering & constructor vs `ngOnInit` |
| 5–6 | Change detection mechanics, `OnPush`, immutability |
| 7–9 | RxJS: cold vs hot, `async` pipe, Observable vs Promise |
| 10–11, 15 | Hierarchical Dependency Injection |
| 12–13 | `@Input()` timing, `*ngFor` diffing/`trackBy` |
| 14 | Template performance, pure pipes |
| 16 | Route guards & async return types |
| 17 | Dev-mode change detection errors |
| 18–20 | Signals: dependency tracking, zoneless CD, effect loops |

**Prep tip:** Interviewers usually escalate along one thread (e.g., start with change detection basics → `OnPush` → Signals → zoneless) rather than jumping randomly. Being able to explain *why* each mechanism exists (not just *what* it does) is what separates a pass from a "we'll get back to you."
