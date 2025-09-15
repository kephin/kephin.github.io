# Type Annotation Basis

## Variable Types

```ts
const name: string = "kevin";
const age: number = 35;
const isEngineer: boolean = true;
```

## Type Inference

Type inference refers to the TypeScript compiler's ability to infer types from certain values in your code.

```ts
const name = "kevin"; // ts infers that 'name' should be a string
```

## The Any Type

`any` turns off type checking for this variable. One thing noticed that the delayed initialization variable will have the implicit any type.

```ts
let anything: any = "anything";
anything = 123;
anything = true;

let dontKnowYet; // ts will infer 'dontKnowYet' to be any
dontKnowYet = "good";
dontKnowYet = 1;
dontKnowYet = true;
```

## Functions

We can specify the type of function parameters and return value in a function definition.

For the code readability, it's better to explicitly put type annotation on return value although it can be inferred by TS in most cases.

```ts
// set default params
function greet(name: string = "stranger"): string {
  return `Hi there, ${name}`;
}

// arrow function
const add = (a: number, b: number): number => a + b;

// void means it doesn't return anything
function print(msg: string): void {
  console.log(msg);
}
```

### Never type

Don't confuse `void` with `never`,

- `void`: returns `undefined` or `null`
- `never`: a function cannot have a reachable end point

```ts
// a function that doesn't finish running
const neverStop = (): never => {
  while (true) {
    console.log("I'm still going!");
  }
};

// a function that throws an exception
const giveError = (msg: string): never => {
  throw new Error(msg);
};
```

## Object Types

Object can be typed by declaring what the object should look like in the annotation.

```ts
// object
const coordinate: { x: number; y: number } = { x: 1, y: 2 };

// function
const printName = ({
  firstName,
  lastName,
}: {
  firstName: string;
  lastName: string;
}): void => {
  console.log(`${firstName} ${lastName}`);
};
```

### Type Alias

Instead of writing out object types in an annotation, we can declare them separately in a type alias, which is simply the desired shape of the object.

```ts
type Person = {
  name: {
    firstName: string,
    lastName: string
  }
  age?: number // optional property
}

const sayHappyBirthday = (person: Person) => { ... }
```

### Read-only Type

```ts
type User = {
  readonly id: number;
  name: string;
};

const user: User = {
  id: 1,
  name: "kevin",
};

user.id = 2; // Cannot assign to 'id' because it is a read-only property.
```

### Intersection Types

An intersection type combines multiple types into one.

```ts
type Colorful = {
  color: string;
};
type Circle = {
  radius: number;
};

const colorfulCircle: Colorful & Circle = {
  color: "green",
  radius: 1.3,
};
```

## Array Types

Array can be typed using a type annotation followed by empty array brackets, like `number[]` for an array of numbers.

```ts
const people: Person[] = [{ name: "kevin", age: 35 }]
// is the same as
const people: Array<Person> = [{ name: "kevin", age: 35 }]

// multi-dimensional arrays
const board = string[][] = [['X', 'O', 'X'], ['X', 'X', 'O'], ['O', 'X', 'X']]
```

## Union Types

Union types allow us to give a value a few different possible types. If the eventual value's type is included, TypeScript will be happy.

```ts
const guessAge = (age: number | string) => `Your age is ${age}`

// all works
guessAge(30)
guessAge("35")

const creatures: (Animal | Plant)[] = [{ animal_1, plant_1, ... }]
```

### Type Narrowing with Union Types

Narrowing the type is simply checking before working with the value.

```ts
const isTeenager = (age: number | string) => {
  if (typeof age === "string") console.log(age.charAt(0) === "1");
  else console.log(age > 12 && age < 20);
};
```

### Literal Types

We can also set type to certain value. Combining it with `unions` can help us fine tune type options.

```ts
const zero: 0 = 0 // zero now can only be 0
type DayOfWeek = ('Monday' | 'Tuesday' | ... | 'Sunday')
const dayOfWeek: DayOfWeek = 'Monday'

const giveAnswer = (answer: "yes" | "no" | "maybe") => `The answer is ${answer}`

giveAnswer("no") // works
giveAnswer("no sure") // not working
```

## Tuples

Tuples are arrays of fixed lengths and ordered with specific types.

```ts
type myTupleType: [number, string]
const myTuple: myTupleType = [10, "kevin"]
```

## Enums

Enums allow us to define a set of named constants.

```ts
// Numeric Enums
enum Responses {
  no, // 0
  yes, // 1
  maybe, // 2
}
enum Responses {
  no = 12,
  yes = 45,
  maybe = 102,
}

// String Enums
enum Response {
  no = "NO",
  yes = "YES",
  maybe = "MAYBE",
}

// Heterogenous
enum Responses {
  no = 0,
  yes = 1,
  maybe = "MAYBE",
}
```

It can be used as Type, as Literal Type.

```ts
enum OrderStatus {
  PENDING,
  SHIPPED,
  DELIVERED,
  RETURNED,
}
const isDelivered = (status: OrderStatus) = status === OrderStatus.DELIVERED
```

### Enum behind the scenes

TypeScript actually compiles `enum` into `object`.

```ts
enum OrderStatus {
  PENDING,
}
const status: OrderStatus.PENDING = OrderStatus.PENDING;

// after compile
("use strict");
var OrderStatus;
(function (OrderStatus) {
  OrderStatus[(OrderStatus["PENDING"] = 0)] = "PENDING";
})(OrderStatus || (OrderStatus = {}));
const status = OrderStatus.PENDING;
```

But we can avoid polluting namespaces by adding `const` in front of the `enum` keyword.

```ts
const enum OrderStatus {
  PENDING,
}
const status: OrderStatus = OrderStatus.PENDING;

// after compile
("use strict");
const status = 0; /* OrderStatus.PENDING */
```

### Issues of `enum`, `const enum`

`enum` can lead to below issues: (check [Don't use Enums in Typescript, they are very dangerous](https://dev.to/ivanzm123/dont-use-enums-in-typescript-they-are-very-dangerous-57bh))

- code size: generates additional code at compile time
- security: numeric enum values are not safe
- compatibility: string enums are a named type and only accept enum-specific values

```ts
// numeric enum
enum Roles {
  Admin,
  Writer,
  Reader,
}
function hasAccess(role: Roles): void;
hasAccess(10); // this is ok! 😱

// string enum
enum Roles {
  Admin = "admin",
  Writer = "writer",
  Reader = "reader",
}
function hasAccess(role: Roles): void;
hasAccess("admin"); // Invalid.
hasAccess(Roles.Admin); // Valid.
```

`const enum` does not support `isolatedModules`. (check [Why are const enums bad?](https://hackmd.io/@dzearing/Sk3xV0cLs))

### Use `as const`

We have to manually create the type.

```ts
const logLevel = {
  DEBUG: "DEBUG",
  WARNING: "WARNING",
  ERROR: "ERROR",
} as const;

type LogLevel = (typeof logLevel)[keyof typeof logLevel];

function doSomeThing(level: LogLevel) {}
doSomeThing(logLevel.DEBUG);
```

## Interfaces

Interfaces serve almost the exact same purpose as type alias. But interface is only used to describe object, not other type of data.

```ts
type name = string;
type light = "red" | "green" | "yellow";
type Person = {
  name: string;
  age: number;
};

interface Product {
  name: string;
  price: number;
}
const disPlayInfo = (product: Product): void => {
  console.log(`${product.name}: ${product.price}`);
};
```

### Readonly, Optional Properties and Methods

```ts
interface Product {
  readonly id: number
  name: string
  size?: string
  price: number
  applyDiscount: (amount: number) => void
  // or
  applyDiscount(amount: number): void
}
const shoes: Product = {
  id: 1,
  name: 'Red wing 9411'
  price: 13000
  applyDiscount(amount) {
    this.price = this.price * (1 - amount)
  }
}
```

### Reopening Interface

```ts
// TS complains about duplicated types
type Person = {
  name: string;
};
type Person = {
  age: number;
};

// the Person interface is the combination of the two
interface Person {
  name: string;
}
interface Person {
  age: number;
}
const me: Person = {
  name: "kevin",
  age: 35,
};
```

### Extends One or More Interfaces

```ts
interface Creature {
  age: number;
}
interface Dog extends Creature {
  name: string;
}
const amy: Dog = {
  name: "Amy",
  age: 1,
};

interface Human {
  name: string;
}
interface Employee {
  readonly id: number;
  email: string;
}
interface Engineer extends Human, Employee {
  level: string;
  languages: string[];
}
const pierre: Engineer = {
  name: "Pierre",
  email: "pierre@gmail.com",
  level: "senior",
  languages: ["JS", "Python"],
};
```

### Types v.s Interfaces

- Interfaces can only describe the shape of `object`
- With `interface`, we can reopen them (add new properties on created interface)
- With `interface`, we use `extends` to extend from other interfaces. But with `type`, we use intersection types with `&`.

```ts
// inheritance
interface Engineer extends Person {
  experience: string;
  languages: string[];
}

// intersection types
type Engineer = Person & {
  experience: string;
  languages: string[];
};
```
