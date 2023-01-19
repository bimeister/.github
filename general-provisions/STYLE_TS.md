## TypeScript (JavaScript) Style Guide

### 1. Only clear and unambiguous names are used.

> Maintainability is the core value of our system code base. – To maintain the code, you need to be able to read it. No need to save symbols, give as much context as needed so that you just need to know the syntax of the language to understand your idea.

```javascript
// 👎 Inalid usage:
arr.reduce((acc, cur) => acc + cur, init);

// 👍 Valid usage:
currentLevelChildrenWeights.reduce(
  (weightSummary, childWeight) => weightSummary + childWeight,
  0
);
```

#### 1.1. `Boolean` clarification:

> Avoid negations in naming variables containing a boolean value. Where possible, you should name such a variable without negation (i.e., without using the prefixes "not", "no", "don't", "never", etc.), and then apply the negation operator `!`.

```typescript
// 👎 Inalid usage:
const hasNoValues: boolean = myArray.length === 0;

// 👍 Valid usage:
const isEmpty: boolean = myArray.length === 0;
```

#### 1.2. `RxJS.Observable` clarification:

> Because `Observables` are a specific part of the project's codebase, governed by special rules and requiring special knowledge, they should be separated from regular language constructs with the `$` suffix.

```typescript
// 👎 Inalid usage:
const activeTabId: Observable<Uuid> = this.tabsService.active;
const currentUserId: Uuid = this.currentUserService.id;

// 👍 Valid usage:
const activeTabId$: Observable<Uuid> = this.tabsService.active$;
const currentUserId: Uuid = this.currentUserService.id;
```

---

### 2. Shorthands in names are not allowed.

...except for the generally accepted names of units of measurement and suffixes described in this document.

| Allowed shorthand | Full form    |
| ----------------- | ------------ |
| ...Param          | ...Parameter |
| ...Ref            | ...Reference |
| ...Arg            | ...Arguments |

```typescript
// 👎 Inalid usage:
const els: Elements[] = [];
const i: number = 0;
const num: number = 0.5;

// 👍 Valid usage:
const elements: Elements[] = [];
const delayMs: number = 10_000;
const constructorParams: unknown[] = [];
```

---

### 3. Values received in the class constructor as arguments cannot have the `public` access modifier.

> The use of public properties in a constructor leads to a violation of encapsulation, and smearing responsibility across code sections.

```typescript
// 👎 Inalid usage:
class {
  constructor(
    public readonly injector: Injector,
    public readonly renderer: Renderer
  ) {}
}

// 👍 Valid usage:
class {
  public readonly injector: Injector,

  constructor(
    injector: Injector,
    private readonly renderer: Renderer
  ) {
    this.injector = injector;
  }
}
```

---

### 4. Only explicit typecasting should be used.

> Explicit type casting increases the readability of the code — you do not need to follow code branches to understand what is being converted into what.

```typescript
// 👎 Inalid usage:
if (!!children && children.length) {
  return children[0];
}

// 👍 Valid usage:
const childrenExist: boolean = Array.isArray(children) && children.length !== 0;
if (childrenExist) {
  return children[0];
}
```

---

### 5. The values of class members should be assigned at the place of declaration, if possible.

> If it is possible to assign a property value at the place of the declaration, you should use it. — The constructor code becomes more compact due to the fact that only expressions that depend on the code that is executed in the constructor remain in it.

```typescript
// 👎 Inalid usage:
class {
  public readonly view: View;

  constructor(private readonly viewBuilder: ViewBuilder) {
    this.view = this.viewBuilder.generate();
  }
}

// 👍 Valid usage:
class {
  public readonly view: View = this.viewBuilder.generate();

  constructor(private readonly viewBuilder: ViewBuilder) {}
}
```

---

### 6. Using `const` is preferable to using `let`.

> Constants are assigned only once, so the code that uses them reads better — no need to return to already read sections after each reassignment.

```typescript
// 👎 Inalid usage:
let item: unknown = undefined;
for (let index = 0; index < source.length; index++) {
  item = source[index];
}

// 👍 Valid usage:
for (let index = 0; index < source.length; index++) {
  const item: unknown = source[index];
}
```

---

### 7. `var` is not allowed.

> Variables created with `var` violate block scope, so they are difficult to control and read.

```typescript
// 👎 Inalid usage:
var APP_STATE: State = EMPTY_STATE;

// 👍 Valid usage:
Object.defineProperty(Window, APP_STATE, { value: EMPTY_STATE });
```

---

### 8. `Enums` name must be a word in the singular form.

> Enum describes several variants of a single value, so it must be named in the singular form.

```typescript
// 👎 Inalid usage:
enum Cities {
  Tokyo,
  Delhi,
  Shanghai,
}
const targetCity: Cities = Cities.Tokyo;

// 👍 Valid usage:
enum City {
  Tokyo,
  Delhi,
  Shanghai,
}
const targetCity: City = City.Tokyo;
```

---

### 9. Access modifiers should not conflict with actual behavior.

> If the `private readonly` value is actually being changed, `readonly` should not be used. \
> If the `private` field is changed from outside, the modifier should be changed to `public`.

```typescript
// 👎 Inalid usage:
class {
  @SetValueTo("World!")
  public readonly displayText: string = "Hello,";
}

// 👍 Valid usage:
class {
  @SetValueTo("World!")
  public displayText: string = "Hello,";
}
```
