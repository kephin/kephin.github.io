# Type Narrowing

## Typeof Guards

`typeof` Type Guards is simply doing type checking before working with a value.

```ts
const isTeenager = (age: (string | number)) => {
    if (typeof age === 'number') {
        return age > 12 && age < 20
    }
    if (typeof age === 'string') {
        return age.charAt(0) === '1'
}
```

## `in` operator narrowing

JavaScript `in` operator helps to check if a certain property exists in an object.

```ts
type Move {
    title: string;
    duration: number;
}
type TVShow = {
    title: string;
    numberOfEpisodes: number;
    episodesDuration: number;
}
const getRunTime = (media: Move | TVShow) => {
    if ('duration' in media) return media.duration
    return media.numberOfEpisodes * media.episodesDuration;
}
```

## `instanceof` narrowing

JavaScript `instanceof` operator to check if one thing is an instance of one class.

```ts
class User {
  constructor(public firstName: string) {}
}
class Company {
  constructor(public name: string) {}
}
const printName = (entity: User | Company) => {
  if (entity instanceof User) {
    console.log(entity.firstName);
  } else {
    console.log(entity.name);
  }
};
```

## Type Predicates

TypeScript allow us to write custom functions that can narrow down the type of a value. These functions have a very special return type called type predicate by `is` keyword.

```ts
interface Cat {
  name: string;
  numLives: number;
}
interface Dog {
  name: string;
  breed: string;
}
const isCat = (pet: Cat | Dog): pet is Cat => {
  return (pet as Cat).numLives !== undefined;
};

const makeNoise = (pet: Cat | Dog): void => {
  if (isCat(pet)) console.log("Meow");
  else console.log("Woof");
};
```

## Discriminated Unions

Creating a `literal` property that is common across multiple types.

```ts
interface Circle {
  kind: "circle";
  radius: number;
}

interface Square {
  kind: "square";
  sideLength: number;
}

type Shape = Circle | Square;

function getArea(shape: Shape) {
  switch shape.kind {
    case 'circle':
      return Math.PI * shape.radius ** 2;
    case 'square'
      return shape.sideLength ** 2;
  }
}
```

## Exhaustive Checking

```ts
function getArea(shape: Shape) {
  switch shape.kind {
    case 'a':
    case 'b'
    case 'c'
    case 'd'
    case 'f'
    // ..
    default:
      // we should never reach this if we handle all the cases correctly
      const _exhaustiveCheck: never = shape;
      return _exhaustiveCheck;
  }
}
```
