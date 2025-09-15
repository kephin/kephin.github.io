# Classes

## Some syntax

- `private` fields: can only have access inside the class
- `super`: during inheritance, to call the constructor function in the parent class

```js
class Player {
  #score = 0;
  constructor(firstName: string, lastName: string) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  getScore() {
    return this.#score;
  }
  setScore(score) {
    this.#score = score;
  }
}

class Admin extends Player {
  constructor(firstName: string, lastName: string, powers: string[]) {
    super(firstName, lastName);
    this.powers = powers;
  }
}
```

## Annotation Classes in TypeScript

Modifiers:

- `readonly`: properties/methods that are not able to be changed once assigned inside the constructor
- `public`: properties/methods that anyone can access and it's default
- `private`: properties/methods that are only accessible inside the class
- `protected`: properties/methods that are only accessible inside the class or in child classes

```ts
class Player {
  public readonly firstName: string;
  public readonly lastName: string;
  private registered = true;
  protected score = 0;

  constructor(firstName: string, lastName: string) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}

class AdminPlayer extends Player {
  maxScore() {
    this.score = 9999; // valid since score is protected property
    this.registered = false; // invalid since registered is private
  }
}

const kevin = new Player("kevin", "hsiao");
kevin.firstName = "allen"; // not working!
```

## Parameter Properties Shorthand

below syntax means we're going to have a public/private property called 'firstName' and it's going to be passed in when player is initialized.

```ts
class Player {
  constructor(public firsName: string, public lastName: string) {}
}
// is equivalent to
class Player {
  public readonly firstName: string;
  public readonly lastName: string;

  constructor(firstName: string, lastName: string) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}
```

## Classes and Interfaces

```ts
interface Colorful {
  color: string;
}
interface Printable {
  print(): void;
}

class Bike implements Colorful, Printable {
  constructor(public color: string) {}
  print() {
    console.log("hello world");
  }
}
```

## Abstract Classes

- abstract class cannot be instantiated
- we can mark `abstract` keyword and all the extended class must implement those abstracted method
- the difference between interface and abstract class is we can provide additional properties/methods from abstract classes

```ts
abstract class Employee {
  constructor(public firstName: string, public lastName: string) {}

  abstract getPay(): number
  greet(){
    console.log('hello')
  }
}

class FulltimeEmployee extends Employee {
  constructor(firstName: string, lastName: string, private salary: number) {
    super(firstName, lastName)
  }
  getPay() { return this.salary }
}
class PartTimeEmployee extends Employee {
  constructor(firstName: string, lastName: string, private hourlyRate: number private hoursWorked: number) {
    super(firstName, lastName)
  }
  getPay() {
    return this.hourlyRate * this.hoursWorked
  }

}
```
