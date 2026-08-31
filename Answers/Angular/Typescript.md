# TypeScript

## Contents
- [What is TypeScript, and why use it instead of plain JavaScript?](#what-is-typescript-and-why-use-it-instead-of-plain-javascript)
- [What are the benefits and tradeoffs of TypeScript?](#what-are-the-benefits-and-tradeoffs-of-typescript)
- [What are key differences between TypeScript and JavaScript?](#what-are-key-differences-between-typescript-and-javascript)
- [Do TypeScript files need compilation, and why?](#do-typescript-files-need-compilation-and-why)
- [What is the difference between .ts and .tsx files?](#what-is-the-difference-between-ts-and-tsx-files)
- [List built-in types in TypeScript.](#list-built-in-types-in-typescript)
- [What is the difference between String and string in TypeScript?](#what-is-the-difference-between-string-and-string-in-typescript)
- [What does the pipe (|) mean in TypeScript?](#what-does-the-pipe--mean-in-typescript)
- [How do you create a string enum?](#how-do-you-create-a-string-enum)
- [What is the difference between enum and const enum?](#what-is-the-difference-between-enum-and-const-enum)
- [What is the difference between declare enum and declare const enum?](#what-is-the-difference-between-declare-enum-and-declare-const-enum)
- [What are modules in TypeScript?](#what-are-modules-in-typescript)
- [What are typings in TypeScript?](#what-are-typings-in-typescript)
- [What are the core components of TypeScript?](#what-are-the-core-components-of-typescript)
- [What is optional chaining (?.), and how is it different from non-null assertion (!)?](#what-is-optional-chaining--and-how-is-it-different-from-non-null-assertion-)
- [What is nullish coalescing (??)?](#what-is-nullish-coalescing-)
- [In a?.b.c, what happens if a.b is null/undefined?](#in-abc-what-happens-if-ab-is-nullundefined)
- [How do you check for null and undefined in TypeScript?](#how-do-you-check-for-null-and-undefined-in-typescript)
- [Which OOP concepts does TypeScript support?](#which-oop-concepts-does-typescript-support)
- [Does TypeScript support function overloading?](#does-typescript-support-function-overloading)
- [How do you overload a class constructor in TypeScript?](#how-do-you-overload-a-class-constructor-in-typescript)
- [How do you call a base class constructor from a child class in TypeScript?](#how-do-you-call-a-base-class-constructor-from-a-child-class-in-typescript)
- [What are getters/setters in TypeScript?](#what-are-getterssetters-in-typescript)
- [What is the default access modifier in a TypeScript class?](#what-is-the-default-access-modifier-in-a-typescript-class)
- [What is the difference between private and protected?](#what-is-the-difference-between-private-and-protected)
- [What is the difference between TypeScript private and ECMAScript #private fields?](#what-is-the-difference-between-typescript-private-and-ecmascript-private-fields)
- [How do you implement class constants in TypeScript?](#how-do-you-implement-class-constants-in-typescript)
- [Why use abstract classes/methods in TypeScript?](#why-use-abstract-classesmethods-in-typescript)
- [How can classes defined in a module be made accessible outside the module?](#how-can-classes-defined-in-a-module-be-made-accessible-outside-the-module)
- [What is an interface in TypeScript?](#what-is-an-interface-in-typescript)
- [When would you use interfaces vs classes?](#when-would-you-use-interfaces-vs-classes)
- [What is the difference between type and interface?](#what-is-the-difference-between-type-and-interface)
- [How do you extend interfaces/types from other interfaces/types?](#how-do-you-extend-interfacestypes-from-other-interfacestypes)
- [How do you do string interpolation in TypeScript?](#how-do-you-do-string-interpolation-in-typescript)
- [Explain generics in TypeScript.](#explain-generics-in-typescript)
- [What is never, and when is it useful?](#what-is-never-and-when-is-it-useful)
- [What is type erasure in TypeScript?](#what-is-type-erasure-in-typescript)
- [What is structural typing?](#what-is-structural-typing)
- [Why is TypeScript called optionally statically typed?](#why-is-typescript-called-optionally-statically-typed)
- [How do you choose between never, unknown, and any?](#how-do-you-choose-between-never-unknown-and-any)
- [What is the difference between unknown and any?](#what-is-the-difference-between-unknown-and-any)
- [What does short-circuiting mean in TypeScript/JavaScript?](#what-does-short-circuiting-mean-in-typescriptjavascript)
- [What are conditional types in TypeScript?](#what-are-conditional-types-in-typescript)
- [What are use cases of template literal types?](#what-are-use-cases-of-template-literal-types)
- [What is unique symbol used for?](#what-is-unique-symbol-used-for)
- [How do you define a class with an index signature in TypeScript, and why use index signatures?](#how-do-you-define-a-class-with-an-index-signature-in-typescript-and-why-use-index-signatures)
- [How do you check a variable’s type in TypeScript?](#how-do-you-check-a-variables-type-in-typescript)
- [How do you make readonly arrays and readonly tuples?](#how-do-you-make-readonly-arrays-and-readonly-tuples)
- [How do you make an array with a specific length or constrained elements in TypeScript?](#how-do-you-make-an-array-with-a-specific-length-or-constrained-elements-in-typescript)
- [Are strongly typed function parameters supported in TypeScript?](#are-strongly-typed-function-parameters-supported-in-typescript)
- [What are assertion functions?](#what-are-assertion-functions)
- [What does const assertion mean, and when is it useful?](#what-does-const-assertion-mean-and-when-is-it-useful)
- [Why is the infer keyword needed in TypeScript?](#why-is-the-infer-keyword-needed-in-typescript)
- [How do you exclude a property from a type in TypeScript?](#how-do-you-exclude-a-property-from-a-type-in-typescript)
- [What are decorators in TypeScript?](#what-are-decorators-in-typescript)
- [How and why would you use property decorators in TypeScript?](#how-and-why-would-you-use-property-decorators-in-typescript)
- [What is a mixin class in TypeScript?](#what-is-a-mixin-class-in-typescript)
- [What is a mixin constructor type?](#what-is-a-mixin-constructor-type)
- [Explain currying in TypeScript.](#explain-currying-in-typescript)
- [What is dynamic import()?](#what-is-dynamic-import)
- [What are import assertions in TypeScript, and what benefits do they provide?](#what-are-import-assertions-in-typescript-and-what-benefits-do-they-provide)
- [Can TypeScript declaration files be generated from a JavaScript library?](#can-typescript-declaration-files-be-generated-from-a-javascript-library)
- [What is a TypeScript source map file?](#what-is-a-typescript-source-map-file)
- [Can TypeScript be used on the backend? How?](#can-typescript-be-used-on-the-backend-how)
- [How do you use external plain JavaScript libraries in TypeScript?](#how-do-you-use-external-plain-javascript-libraries-in-typescript)
- [What are ambient declarations, and when do you use declare?](#what-are-ambient-declarations-and-when-do-you-use-declare)
- [What does tsconfig "lib" option do?](#what-does-tsconfig-lib-option-do)
- [What is the purpose of --incremental in TypeScript?](#what-is-the-purpose-of---incremental-in-typescript)
- [How do you create a union type from type alias or interface properties?](#how-do-you-create-a-union-type-from-type-alias-or-interface-properties)
- [Explain project references and their benefits.](#explain-project-references-and-their-benefits)
- [How does the override keyword work in TypeScript?](#how-does-the-override-keyword-work-in-typescript)

---

## What is TypeScript, and why use it instead of plain JavaScript?
TypeScript is a superset of JavaScript that adds static typing and tooling features on top of standard JS. It helps catch many errors at compile time before code reaches production. The type system improves readability, maintainability, and onboarding for larger teams. It also provides excellent IDE support like autocomplete, refactoring, and jump-to-definition. You still write JavaScript-compatible code, but with safer contracts and clearer intent.

```ts
function greet(name: string): string {
  return `Hello, ${name}`;
}

const msg = greet('Sam');
```

---

## What are the benefits and tradeoffs of TypeScript?
The biggest benefits are early error detection, better editor tooling, and self-documenting APIs. It scales well for large codebases because types reduce accidental breaking changes. TypeScript also makes refactoring safer and easier over time. Tradeoffs include extra setup, a compile step, and learning advanced type features. In small scripts, strict typing may feel like overhead if the code is short-lived.

```ts
interface User {
  id: number;
  name: string;
}

const u: User = { id: 1, name: 'Ana' };
```

---

## What are key differences between TypeScript and JavaScript?
JavaScript is dynamically typed, while TypeScript adds optional static typing and compile-time checks. TypeScript supports interfaces, enums, generics, and utility types that JavaScript does not have natively. JS runs directly in engines, but TS must be transpiled to JavaScript first. TypeScript tooling gives stronger autocomplete and safer refactoring in IDEs. At runtime, both are JavaScript, because TypeScript types are erased.

```ts
// TypeScript catches this at compile-time
let total: number = 10;
// total = '10'; // error
```

---

## Do TypeScript files need compilation, and why?
Yes, TypeScript files are compiled (transpiled) into JavaScript before execution. Browsers and Node runtimes execute JavaScript, not raw TypeScript syntax. The compiler removes types and transforms newer features based on target settings. During this process, it also performs type checking and reports errors. This compile step is the reason TypeScript can enforce strong static analysis.

```ts
// input.ts
const value: number = 42;

// output.js (conceptually)
const value = 42;
```

---

## What is the difference between .ts and .tsx files?
`.ts` is for regular TypeScript files without JSX syntax. `.tsx` is used when TypeScript code includes JSX/TSX markup, usually in React projects. Both support types, interfaces, and generics equally. The main difference is parser behavior for angle-bracket syntax and JSX elements. If you write UI with JSX, use `.tsx`; otherwise `.ts` is preferred.

```tsx
type Props = { title: string };

function Header({ title }: Props) {
  return <h1>{title}</h1>;
}
```

---

## List built-in types in TypeScript.
Common primitive types are `string`, `number`, `boolean`, `bigint`, `symbol`, `null`, and `undefined`. Important special types include `any`, `unknown`, `never`, and `void`. You also use object-related forms like `object`, arrays, tuples, and function types. Literal and union types are built from these core pieces. Knowing these basics is essential before advanced generics.

```ts
let name: string = 'Tom';
let count: number = 3;
let done: boolean = false;
let data: unknown = { ok: true };
```

---

## What is the difference between String and string in TypeScript?
`string` is the primitive type and should be used in almost all TypeScript code. `String` is the boxed object wrapper type and is rarely what you want. Using wrapper object types can lead to confusing behavior and weaker type expectations. TypeScript style guides generally recommend primitive lowercase types. So prefer `string`, `number`, and `boolean` over `String`, `Number`, and `Boolean`.

```ts
let a: string = 'hello';
let b: String = new String('hello');

const ok: string = a;
```

---

## What does the pipe (|) mean in TypeScript?
The pipe creates a union type, meaning a value can be one of multiple allowed types. Unions improve flexibility while still keeping type safety. They are often used for API responses, function parameters, and discriminated unions. You usually narrow union types with checks before using specific members. This is safer than `any` because the compiler enforces handling all possibilities.

```ts
function printId(id: string | number): void {
  if (typeof id === 'string') {
    console.log(id.toUpperCase());
  }
}
```

---

## How do you create a string enum?
You define enum members and assign string literals as values. String enums are useful for readable logs, API payloads, and stable serialized values. They avoid numeric reverse-mapping behavior and make debugging easier. They also prevent typo-prone magic strings when used consistently. Keep enum names focused on one domain concept.

```ts
enum Status {
  Pending = 'PENDING',
  Success = 'SUCCESS',
  Failed = 'FAILED'
}
```

---

## What is the difference between enum and const enum?
Regular `enum` exists at runtime as an object and can be inspected. `const enum` is inlined at compile time and usually emits no enum object. This can reduce runtime overhead and bundle size in some builds. The tradeoff is less runtime reflection and potential tooling constraints in isolated transpilation setups. Use `const enum` only when your build pipeline supports it safely.

```ts
enum Role {
  Admin,
  User
}

const enum FastRole {
  Admin,
  User
}
```

---

## What is the difference between declare enum and declare const enum?
`declare enum` describes an enum shape that exists elsewhere at runtime. `declare const enum` tells TypeScript to inline values and assume no runtime object is needed. Both are ambient declarations, typically used in `.d.ts` files. The key difference is emitted access behavior and runtime expectation. Use `declare const enum` only when external values are compile-time stable.

```ts
// in a .d.ts file
declare enum ApiMode {
  Dev,
  Prod
}
```

---

## What are modules in TypeScript?
Modules are files that export and import code to create explicit boundaries. They prevent global namespace pollution and make dependencies clear. ES modules are the standard format in modern TypeScript projects. A file becomes a module as soon as it has an `import` or `export`. Modules improve maintainability and support tree-shaking in bundlers.

```ts
// math.ts
export function add(a: number, b: number): number {
  return a + b;
}
```

---

## What are typings in TypeScript?
Typings are type definitions that describe the shape of JavaScript code for the TypeScript compiler. They allow type-safe use of libraries written in plain JavaScript. Typings usually come from bundled `.d.ts` files or `@types/*` packages. Good typings significantly improve editor intelligence and compile-time safety. Without typings, many external APIs degrade to `any`.

```ts
// npm i -D @types/lodash
import _ from 'lodash';

const out = _.chunk([1, 2, 3, 4], 2);
```

---

## What are the core components of TypeScript?
Core pieces include the type system, compiler (`tsc`), and language service used by IDEs. The type system covers primitives, unions, generics, interfaces, and utility types. The compiler checks types and transpiles TS to JS based on `tsconfig`. Declaration files (`.d.ts`) enable typed interop with external code. Together, these components provide both runtime compatibility and strong developer tooling.

```ts
// tsconfig.json (conceptual keys)
// { "compilerOptions": { "strict": true, "target": "ES2020" } }
```

---

## What is optional chaining (?.), and how is it different from non-null assertion (!)?
Optional chaining safely stops access when a value is `null` or `undefined`, returning `undefined`. Non-null assertion tells the compiler to trust you that a value is not nullish. `?.` adds runtime safety, while `!` only suppresses compile-time checks. Overusing `!` can hide real null bugs and create runtime failures. Prefer `?.` when uncertainty is real, and use `!` only when you have strong guarantees.

```ts
type User = { profile?: { city?: string } };

const user: User = {};
const city = user.profile?.city;
```

---

## What is nullish coalescing (??)?
`??` returns the right-hand value only when the left side is `null` or `undefined`. It is safer than `||` when `0`, `''`, or `false` are valid values you want to keep. This makes defaults more precise and less bug-prone. It is commonly combined with optional chaining in real code. Use it for fallback values without treating all falsy values as missing.

```ts
const page = 0;
const current = page ?? 1; // stays 0
```

---

## In a?.b.c, what happens if a.b is null/undefined?
Only `a` is protected in `a?.b.c`; the rest of the chain is not automatically safe. If `a` is nullish, result is `undefined` and evaluation stops. If `a` exists but `a.b` is nullish, then `.c` access can throw at runtime. To protect each uncertain hop, use `a?.b?.c`. This is a common interview trick around optional chaining scope.

```ts
const x: any = { b: null };
// const v = x?.b.c; // runtime error
const safe = x?.b?.c; // undefined
```

---

## How do you check for null and undefined in TypeScript?
Use `value == null` to check both `null` and `undefined` in one expression. Use strict checks (`=== null` or `=== undefined`) when you need to distinguish them. Type narrowing works well with guard clauses in functions. For object fields, optional chaining and nullish coalescing keep checks concise. Enabling `strictNullChecks` is critical for reliable behavior.

```ts
function normalize(v: string | null | undefined): string {
  if (v == null) return 'N/A';
  return v.trim();
}
```

---

## Which OOP concepts does TypeScript support?
TypeScript supports encapsulation, inheritance, polymorphism, and abstraction. You can model these using classes, access modifiers, abstract classes, and interfaces. It also supports method overriding and implementation contracts. Multiple inheritance is not supported for classes, but interfaces can be composed. OOP in TS is optional and can coexist with functional patterns.

```ts
abstract class Animal {
  abstract speak(): void;
}

class Dog extends Animal {
  speak(): void {
    console.log('Woof');
  }
}
```

---

## Does TypeScript support function overloading?
Yes, TypeScript supports function overloading through multiple signatures and one implementation. Overload signatures describe valid call patterns visible to callers. The implementation signature is broader and handles all cases internally. This improves API clarity while preserving type safety. It is useful when behavior depends on input types.

```ts
function format(value: number): string;
function format(value: Date): string;
function format(value: number | Date): string {
  return value instanceof Date ? value.toISOString() : value.toFixed(2);
}
```

---

## How do you overload a class constructor in TypeScript?
You define multiple constructor signatures and then one implementation constructor. The implementation accepts a union or optional params and branches at runtime. This pattern simulates constructor overloading while keeping type-safe call sites. It is common in SDK clients and value objects. Keep overloads minimal to avoid confusing APIs.

```ts
class Point {
  x: number;
  y: number;

  constructor(x: number, y: number);
  constructor(coords: [number, number]);
  constructor(a: number | [number, number], b?: number) {
    if (Array.isArray(a)) {
      [this.x, this.y] = a;
    } else {
      this.x = a;
      this.y = b ?? 0;
    }
  }
}
```

---

## How do you call a base class constructor from a child class in TypeScript?
Use `super(...)` inside the child constructor. In derived classes, `super` must be called before accessing `this`. The base constructor can initialize shared fields and validation logic. This enforces proper inheritance initialization order. It is the same conceptual rule as modern JavaScript classes.

```ts
class Person {
  constructor(public name: string) {}
}

class Employee extends Person {
  constructor(name: string, public id: number) {
    super(name);
  }
}
```

---

## What are getters/setters in TypeScript?
Getters and setters are property accessors that wrap field reads and writes. They let you enforce validation or computed behavior while keeping property-like syntax. This supports encapsulation without exposing raw internal state. You can make one accessor readonly by omitting a setter. Use accessors when logic is needed, not for trivial passthroughs.

```ts
class User {
  private _age = 0;

  get age(): number {
    return this._age;
  }

  set age(value: number) {
    if (value >= 0) this._age = value;
  }
}
```

---

## What is the default access modifier in a TypeScript class?
Class members are `public` by default in TypeScript. That means they are accessible from outside the class unless marked otherwise. You can explicitly use `private`, `protected`, or `readonly` as needed. Being explicit can improve readability in shared codebases. For API surfaces, thoughtful access levels reduce accidental coupling.

```ts
class Account {
  id = 1; // public by default
  private token = 'secret';
}
```

---

## What is the difference between private and protected?
`private` members are only accessible within the declaring class. `protected` members are accessible in the class and its subclasses. Neither is accessible from outside instances directly. Choose `protected` when child classes need extension points. Choose `private` for strictly internal implementation details.

```ts
class Base {
  private a = 1;
  protected b = 2;
}

class Child extends Base {
  read(): number {
    return this.b;
  }
}
```

---

## What is the difference between TypeScript private and ECMAScript #private fields?
TypeScript `private` is enforced by the compiler, but it becomes normal property names at runtime. ECMAScript `#private` fields are enforced by JavaScript runtime semantics. That means `#private` cannot be accessed even with bracket notation from outside. `private` is useful for type-level design, while `#private` adds stronger runtime privacy. Modern projects may use either based on target compatibility and style.

```ts
class Box {
  private secret = 'ts-private';
  #hardSecret = 'js-private';

  reveal(): string {
    return this.secret + ' / ' + this.#hardSecret;
  }
}
```

---

## How do you implement class constants in TypeScript?
Use `readonly` for instance constants and `static readonly` for class-level constants. `readonly` allows assignment only during declaration or constructor initialization. `static readonly` is ideal for shared fixed values like limits or version strings. This prevents accidental reassignment while keeping clear intent. For immutable groups, combine with `as const` objects when appropriate.

```ts
class Config {
  static readonly APP_NAME = 'Portal';
  readonly createdAt = new Date();
}
```

---

## Why use abstract classes/methods in TypeScript?
Abstract classes define shared structure and partial implementation for related subclasses. Abstract methods enforce contracts that children must implement. This reduces duplication while preserving flexibility for specific behavior. They are useful when you need both shared code and required extension points. Unlike interfaces, abstract classes can include implemented members and state.

```ts
abstract class Repository<T> {
  abstract findById(id: string): T | null;

  log(msg: string): void {
    console.log(msg);
  }
}
```

---

## How can classes defined in a module be made accessible outside the module?
Export the class from its module and import it where needed. You can use named exports for most cases and default export sparingly. Public APIs are often re-exported from an index barrel file. This keeps dependency boundaries explicit and discoverable. Module exports are the standard way to share class implementations.

```ts
// user.service.ts
export class UserService {}

// app.ts
import { UserService } from './user.service';
```

---

## What is an interface in TypeScript?
An interface defines the shape of an object, function, or class contract. It specifies required members without providing implementation. Interfaces improve consistency between producers and consumers of data. They are especially useful for API models and dependency boundaries. Interfaces exist only at compile time and have no runtime footprint.

```ts
interface Product {
  id: number;
  name: string;
}

const p: Product = { id: 1, name: 'Book' };
```

---

## When would you use interfaces vs classes?
Use interfaces to define contracts and data shapes without implementation. Use classes when you need behavior, state, constructors, or inheritance logic. Interfaces are lightweight and great for decoupling layers. Classes are better for reusable logic and instantiation. In many systems, interfaces define boundaries and classes implement them.

```ts
interface Notifier {
  send(msg: string): void;
}

class EmailNotifier implements Notifier {
  send(msg: string): void {
    console.log('email:', msg);
  }
}
```

---

## What is the difference between type and interface?
Both can describe object shapes, but they have different strengths. `interface` supports declaration merging and is often preferred for public object contracts. `type` supports unions, intersections, mapped types, and primitives aliasing more naturally. Interfaces are usually more readable for OOP-style API design. Types are more flexible for advanced type transformations.

```ts
interface User {
  id: number;
}

type UserId = string | number;
```

---

## How do you extend interfaces/types from other interfaces/types?
Interfaces use `extends` to inherit members from one or more interfaces. Type aliases usually use intersections (`&`) to compose shapes. You can also extend a type-like object shape with another interface in many cases. Composition keeps models DRY and consistent. Be careful with conflicting property types during merges.

```ts
interface A {
  id: number;
}

interface B extends A {
  name: string;
}

type C = A & { active: boolean };
```

---

## How do you do string interpolation in TypeScript?
Use template literals with backticks and `${}` placeholders. This is standard JavaScript syntax and fully supported in TypeScript. It is cleaner than concatenation for readability. You can interpolate variables and expressions directly. Template literals are also useful with tagged templates in advanced cases.

```ts
const user = 'Lee';
const score = 95;
const text = `User ${user} scored ${score}`;
```

---

## Explain generics in TypeScript.
Generics let you write reusable code while preserving strong type information. Instead of hardcoding one type, you use type parameters like `<T>`. The compiler infers or enforces concrete types at usage points. This avoids duplication and keeps APIs flexible yet safe. Generics are foundational in collections, utility functions, and framework APIs.

```ts
function first<T>(arr: T[]): T | undefined {
  return arr[0];
}

const v = first<number>([10, 20]);
```

---

## What is never, and when is it useful?
`never` represents values that should never occur. It is used for functions that always throw or never return, and for exhaustive checks. In union narrowing, assigning remaining cases to `never` catches unhandled variants. This is very useful in reducers and discriminated unions. `never` improves correctness by enforcing impossible states.

```ts
type Shape = { kind: 'circle' } | { kind: 'square' };

function area(s: Shape): number {
  switch (s.kind) {
    case 'circle': return 1;
    case 'square': return 2;
    default: {
      const _exhaustive: never = s;
      return _exhaustive;
    }
  }
}
```

---

## What is type erasure in TypeScript?
Type erasure means TypeScript types are removed during compilation. Runtime JavaScript does not keep interfaces, generics, or most annotations. Because of this, type checks are compile-time only unless you add runtime validation. Developers often combine TS with schema validators for external data. Understanding erasure prevents false assumptions about runtime safety.

```ts
function echo<T>(value: T): T {
  return value;
}

// emitted JS has no <T> information
```

---

## What is structural typing?
Structural typing means compatibility is based on shape, not explicit declarations. If an object has required properties, it can satisfy a type. This is different from nominal systems that require explicit class inheritance. Structural typing makes interop flexible but may allow accidental compatibility. Narrow interfaces and branded types can reduce such risks.

```ts
interface HasName {
  name: string;
}

const obj = { name: 'Neo', age: 30 };
const x: HasName = obj;
```

---

## Why is TypeScript called optionally statically typed?
TypeScript allows static types but does not force full annotation everywhere. You can progressively add types to existing JavaScript code. Type inference automatically derives many types without explicit annotations. You may still use `any` or JS files when needed, reducing migration friction. This optional nature makes adoption practical for teams of different maturity.

```ts
let x = 10; // inferred as number
let y: any = 'unsafe';
```

---

## How do you choose between never, unknown, and any?
Use `any` only when you intentionally opt out of type safety. Use `unknown` for values you do not trust yet and narrow before usage. Use `never` for impossible outcomes, exhaustive checks, or non-returning functions. A good rule is: prefer `unknown`, avoid `any`, and use `never` for logic guarantees. This keeps APIs honest and safer.

```ts
function fail(msg: string): never {
  throw new Error(msg);
}

function parse(input: unknown): string {
  if (typeof input === 'string') return input;
  return 'invalid';
}
```

---

## What is the difference between unknown and any?
`any` disables type checking and allows any operation. `unknown` accepts any value but requires narrowing before using it. So `unknown` is the safer top type for untrusted inputs. It forces explicit guards and prevents accidental runtime errors. Prefer `unknown` for external data boundaries.

```ts
let a: any = 10;
a.toUpperCase(); // no compile error, risky

let b: unknown = 10;
// b.toUpperCase(); // compile error until narrowed
```

---

## What does short-circuiting mean in TypeScript/JavaScript?
Short-circuiting means logical operators stop evaluation as soon as result is determined. `&&` stops when left side is falsy, `||` stops when left is truthy, and `??` stops when left is non-nullish. It is often used for guards and fallback values. While concise, overuse can reduce readability if expressions get dense. Prefer clarity when writing business-critical conditions.

```ts
const user = { name: 'A' } as { name?: string } | null;
const label = user && user.name ? user.name : 'Guest';
const title = user?.name ?? 'Guest';
```

---

## What are conditional types in TypeScript?
Conditional types choose one type or another based on a compile-time condition. They use `T extends U ? X : Y` syntax. This enables reusable type-level logic and adaptive APIs. Many utility types like `Exclude` and `ReturnType` rely on this mechanism. They are powerful but should be kept readable to avoid maintenance pain.

```ts
type IsString<T> = T extends string ? true : false;

type A = IsString<'x'>;  // true
type B = IsString<42>;   // false
```

---

## What are use cases of template literal types?
Template literal types build new string types from other string unions. They are useful for typed event names, route keys, CSS utility names, and API conventions. This improves autocomplete and prevents typo bugs in string-heavy APIs. They can also combine with mapped types for strongly typed dictionaries. Overly complex constructions should be avoided for readability.

```ts
type EventName<T extends string> = `${T}Changed`;

type UserEvents = EventName<'name' | 'email'>;
// 'nameChanged' | 'emailChanged'
```

---

## What is unique symbol used for?
`unique symbol` creates a symbol type that is guaranteed to be distinct. It is useful for branded keys, nominal typing tricks, and collision-free constants. Unlike regular `symbol`, each unique symbol has its own specific type. This helps enforce stricter contracts in advanced libraries. It is mainly used in framework or infrastructure-level code.

```ts
declare const TOKEN: unique symbol;

type Tokenized = {
  [TOKEN]: string;
};
```

---

## How do you define a class with an index signature in TypeScript, and why use index signatures?
An index signature allows dynamic property names with known value types. In classes, you can define `[key: string]: T` to model dictionary-like behavior. It is useful when keys are not known at compile time but values have a consistent shape. Be careful because broad index signatures can weaken strict typing of specific fields. Prefer narrower mapped types when keys are known unions.

```ts
class Store {
  [key: string]: string | number;

  version = 1;
  name = 'main';
}
```

---

## How do you check a variable’s type in TypeScript?
Use runtime guards like `typeof`, `instanceof`, and `in` for narrowing. You can also create custom type predicates for reusable checks. The compiler uses these guards to narrow union types safely. For external JSON, runtime validation libraries are often needed beyond basic guards. Good narrowing patterns reduce unsafe assertions.

```ts
function isDate(v: unknown): v is Date {
  return v instanceof Date;
}

function print(v: string | number): void {
  if (typeof v === 'string') console.log(v.toUpperCase());
}
```

---

## How do you make readonly arrays and readonly tuples?
Use `readonly T[]` or `ReadonlyArray<T>` for arrays. For tuples, prefix with `readonly` to freeze element reassignment at type level. This prevents mutation and helps enforce immutability patterns. It is useful for function parameters and shared constants. Remember this is compile-time protection, not deep runtime immutability.

```ts
const nums: readonly number[] = [1, 2, 3];
const pair: readonly [string, number] = ['id', 10];
```

---

## How do you make an array with a specific length or constrained elements in TypeScript?
TypeScript cannot fully enforce dynamic runtime array length, but tuples enforce fixed length at compile time. For constrained elements, use union types or branded helper types. You can also create factory functions that validate length at runtime and return branded types. This combines runtime safety with compile-time expressiveness. For exact lengths, tuples are the simplest first choice.

```ts
type RGB = [number, number, number];

const color: RGB = [255, 128, 64];
// const bad: RGB = [255, 0]; // error
```

---

## Are strongly typed function parameters supported in TypeScript?
Yes, function parameters can be strongly typed with primitives, interfaces, unions, generics, and function types. This lets the compiler validate call sites and argument shapes. Optional and default parameters are also type-checked. Strong parameter typing improves API discoverability and reduces runtime checks. It is one of TypeScript’s most practical benefits.

```ts
function createUser(name: string, age: number, active = true): void {
  console.log(name, age, active);
}
```

---


## What are assertion functions?
Assertion functions tell TypeScript that a condition is true after the function returns. They use `asserts` in the return type and enable type narrowing. This is useful for validating external input at boundaries. If assertion fails, the function usually throws an error. Assertion functions improve safety while keeping call-site code clean.

```ts
function assertString(value: unknown): asserts value is string {
  if (typeof value !== 'string') {
    throw new Error('Expected string');
  }
}
```

---

## What does const assertion mean, and when is it useful?
`as const` makes literal values as narrow as possible and marks object properties readonly. Arrays become readonly tuples, and strings stay literal types instead of widening to `string`. This is useful for config objects, action types, and exhaustive unions. It improves inference quality without verbose annotations. Use it when values are intended to be immutable constants.

```ts
const config = {
  env: 'prod',
  retries: 3
} as const;
```

---

## Why is the infer keyword needed in TypeScript?
`infer` lets you capture a type variable inside conditional types. It enables extraction patterns like return types, element types, or promise payloads. Without `infer`, many type transformations would be much harder or impossible to express cleanly. It is heavily used in advanced utility types. Keep inferred type logic simple for maintainability.

```ts
type ElementType<T> = T extends (infer U)[] ? U : never;

type A = ElementType<string[]>; // string
```

---

## How do you exclude a property from a type in TypeScript?
Use `Omit<T, K>` to remove keys from an existing type. You can also combine `Pick`, `Exclude`, and mapped types for custom transforms. This is helpful for DTOs, API input/output shaping, and privacy constraints. It avoids duplicating near-identical type declarations. Utility types keep type modeling DRY and consistent.

```ts
interface User {
  id: number;
  name: string;
  password: string;
}

type PublicUser = Omit<User, 'password'>;
```

---

## What are decorators in TypeScript?
Decorators are annotations that can add metadata or wrap behavior around classes and members. They are common in frameworks like Angular and NestJS. Decorators can target classes, methods, accessors, properties, or parameters. They are powerful but should be used carefully to avoid hidden complexity. Support depends on compiler options and proposal stage compatibility.

```ts
function Sealed<T extends { new (...args: any[]): {} }>(ctor: T): T {
  Object.seal(ctor);
  Object.seal(ctor.prototype);
  return ctor;
}

@Sealed
class Service {}
```

---

## How and why would you use property decorators in TypeScript?
Property decorators can attach metadata to class fields for validation, DI, or serialization logic. They are often used by frameworks to discover configuration declaratively. This reduces boilerplate and keeps intent close to the property definition. However, decorators can hide control flow, so they should be documented and tested. Use them when framework conventions justify the abstraction.

```ts
function Required(target: object, key: string): void {
  Reflect.defineMetadata('required', true, target, key);
}

class CreateUserDto {
  @Required
  email!: string;
}
```

---

## What is a mixin class in TypeScript?
A mixin is a pattern for composing reusable behavior into classes without deep inheritance trees. You define a function that takes a base class and returns an extended class. This supports horizontal code reuse and modular features. Mixins are useful for cross-cutting abilities like timestamping or logging. Keep mixins focused and avoid stacking too many for readability.

```ts
type Ctor<T = {}> = new (...args: any[]) => T;

function Timestamped<TBase extends Ctor>(Base: TBase) {
  return class extends Base {
    createdAt = new Date();
  };
}
```

---

## What is a mixin constructor type?
A mixin constructor type describes a class constructor shape accepted by mixin functions. It is usually written as `new (...args: any[]) => T`. This allows generic mixins to work with many base classes safely. Without this constraint, composing mixins becomes difficult to type correctly. It is a core building block of typed class composition.

```ts
type Constructor<T = {}> = new (...args: any[]) => T;

function WithId<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    id = crypto.randomUUID();
  };
}
```

---

## Explain currying in TypeScript.
Currying transforms a function with multiple arguments into chained unary functions. It enables partial application and reusable specialized functions. In TypeScript, generics help preserve type information across each step. Currying is useful in functional pipelines and dependency injection style helpers. Overuse can reduce readability if the team is not familiar with the pattern.

```ts
const add = (a: number) => (b: number) => a + b;

const addFive = add(5);
const result = addFive(3);
```

---

## What is dynamic import()?
`import()` loads modules asynchronously at runtime and returns a promise. It enables lazy loading and smaller initial bundles. This is useful for route-based splitting and optional heavy features. Dynamic import is standard ECMAScript and works with modern bundlers. In TypeScript, imported module types are still inferred correctly.

```ts
async function loadMath() {
  const mod = await import('./math');
  return mod.add(1, 2);
}
```

---

## What are import assertions in TypeScript, and what benefits do they provide?
Import assertions add metadata about expected module type, such as JSON. They improve clarity and can enable stricter loading semantics in compatible environments. This reduces ambiguity and certain classes of loading mistakes. TypeScript can type-check imported JSON shape when configured properly. Support varies by runtime and bundler, so compatibility should be verified.

```ts
import data from './config.json' assert { type: 'json' };

console.log(data);
```

---

## Can TypeScript declaration files be generated from a JavaScript library?
Yes, TypeScript can generate declaration files from JavaScript with JSDoc annotations. You can enable `allowJs`, `checkJs`, and `declaration` in compiler options. This helps gradually type existing JS libraries without full rewrite. Generated `.d.ts` files improve consumer tooling and safety. Manual cleanup may still be needed for complex dynamic APIs.

```ts
// tsconfig.json (conceptual)
// { "compilerOptions": { "allowJs": true, "declaration": true, "emitDeclarationOnly": true } }
```

---

## What is a TypeScript source map file?
A source map links generated JavaScript back to original TypeScript sources. It allows debuggers to show TS lines and variable names during runtime debugging. Source maps make breakpoints and stack traces much more useful. They are essential in development and can be controlled separately for production. Keep production source-map strategy aligned with security and troubleshooting needs.

```ts
// tsconfig.json
// { "compilerOptions": { "sourceMap": true } }
```

---

## Can TypeScript be used on the backend? How?
Yes, TypeScript is widely used on backend platforms like Node.js. You can run compiled JS output with Node, or use tools like ts-node for development. Popular frameworks include NestJS, Express with TS, and Fastify with TS. Strong typing improves API contracts, service boundaries, and refactoring safety. Build pipelines usually transpile TS during CI/CD before deployment.

```ts
import express from 'express';

const app = express();
app.get('/health', (_req, res) => res.send('ok'));
app.listen(3000);
```

---

## How do you use external plain JavaScript libraries in TypeScript?
Install typings if available (usually `@types/...`) and import normally. If typings do not exist, create custom declaration files for required API surface. Start with minimal declarations and refine as needed. Avoid declaring everything as `any`, because it removes safety benefits. This approach enables gradual, practical interop with legacy JS packages.

```ts
// custom.d.ts
declare module 'legacy-lib' {
  export function run(task: string): void;
}
```

---

## What are ambient declarations, and when do you use declare?
Ambient declarations describe entities that exist at runtime but are implemented elsewhere. They are written with `declare` and usually live in `.d.ts` files. Use them for global variables, external scripts, or untyped libraries. Ambient types provide compile-time knowledge without generating code. They are key to integrating TypeScript with non-TS ecosystems.

```ts
declare const APP_VERSION: string;

declare function track(event: string): void;
```

---

## What does tsconfig "lib" option do?
The `lib` option selects built-in type definitions for JavaScript environments and features. Examples include `ES2022`, `DOM`, and `WebWorker`. It controls which global APIs TypeScript knows about during type checking. If a needed API is missing, adding the right lib fixes type errors. Keep `lib` aligned with your runtime targets to avoid false assumptions.

```ts
// tsconfig.json
// {
//   "compilerOptions": { "lib": ["ES2022", "DOM"] }
// }
```

---

## What is the purpose of --incremental in TypeScript?
`--incremental` stores build metadata to speed up subsequent compilations. On later builds, TypeScript recompiles only changed parts when possible. This is especially valuable in large projects and CI pipelines with caching. It improves feedback loops during development. The metadata is typically saved in a `.tsbuildinfo` file.

```ts
// shell command
// tsc --incremental
```

---

## How do you create a union type from type alias or interface properties?
You can index into property keys to produce a union of property value types. `keyof` plus indexed access types are common tools for this. This technique is useful for generic utilities and schema-driven APIs. It keeps unions in sync with source models automatically. It avoids repeating literal unions manually.

```ts
interface Person {
  name: string;
  age: number;
}

type PersonValue = Person[keyof Person]; // string | number
```

---

## Explain project references and their benefits.
Project references split large TypeScript codebases into smaller buildable units. Each subproject can compile independently and emit declarations for dependents. This improves build speed, modularity, and architectural boundaries. Editors also perform better in monorepos using references. They are configured with `composite` and `references` entries in tsconfig files.

```ts
// tsconfig.json (conceptual)
// {
//   "files": [],
//   "references": [{ "path": "./packages/core" }, { "path": "./packages/app" }]
// }
```

---

## How does the override keyword work in TypeScript?
`override` marks that a subclass method intentionally overrides a base class member. The compiler verifies that the base member actually exists and is overridable. This prevents accidental shadowing from typos or API drift. It improves safety during refactoring in inheritance-heavy code. Enabling `noImplicitOverride` enforces this practice consistently.

```ts
class Base {
  greet(): string {
    return 'hi';
  }
}

class Child extends Base {
  override greet(): string {
    return 'hello';
  }
}
```

---
