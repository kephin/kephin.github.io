# Generics

Generics allow us to define reusable functions and classes that work with multiple types rather than a single type.

## Built-in Generics

It's kind of like a type argument.

```ts
const numbers: Array<number> = [];
// is equal to
const numbers: number[] = [];

// TypeScript only knows it's a general element
const element = document.querySelector("#username")!;
// Now TypeScript knows it's an HTMLInputElement
const inputElement = document.querySelector<HTMLInputElement>("#username")!;
```

## When Should We Use Generics?

```ts
function func<T>(element: T): T[] {
  return [element];
}

// [1, 2, 3, 4, 5, ...]
// [true, false, false, ...]
// [{}, {}, {}, ..]
function getRandomElement<T>(list: T[]): T {
  const randomIndex = Math.floor(Math.random() * list.length);
  return list[randomIndex];
}

getRandomElement<string>(["a", "b", "c", "d"]); // -> maybe'c'
getRandomElement<number>([1, 23, 255, 332, 6433]); // -> maybe 255
```

## Inferred Generic Type Parameters

TypeScript can infer the type, but not always.

```ts
getRandomElement(["a", "b", "c", "d"]);
```

## Generics Arrow Functions & .tsx files

In .tsx, we have to add a trailing comma in order to make TypeScript understand the generics syntax(in order to be distinguished from html tag).

```ts
const App = <T,>(list: T[]) => {
  return {list.map(item => (
    <div>{item.name}</div>
  ))}
}
```

## Generics with Multiple Types

We don't have to tell TypeScript what it will return because TypeScript will infer.

```ts
const merge = <T, U>(object1: T, object2: U) => ({
  ...object1,
  ...object2,
});
// no need to
const merge = <T, U>(object1: T, object2: U): T & U => {
  // ...
};

const comboObject = merge(
  { name: "kevin" },
  { languages: ["javascript", "typescript", "go", "ruby", "python"] }
);
```

## Add Type Constraints

We can add type constrains in order to make sure `merge` only have `object` arguments.

```ts
// TypeScript doesn't know what's the type of argument, so won't complain on this line
merge({ name: "kevin" }, 10);

// in order make TypeScript know, we can add constraints into generic types
const merge = <T extends object, U extends object>(object1: T, object2: U) => ({
  ...object1,
  ...object2,
});
// or just
const merge = (object1: object, object2: object) => ({
  ...object1,
  ...object2,
});

// we can also use custom interface
interface Lengthy {
  length: number;
}
const printDoubleLength = <T extends Lengthy>(thing: T): number => {
  return thing.length * 2;
};
// or just
const printDoubleLength = (thing: Lengthy): number => {
  return thing.length * 2;
};
```

## Default Type Parameters

```ts
const makeEmptyArray = <T = string>(): T[] => [];
const strings = makeEmptyArray();
const numbers = makeEmptyArray<number>();
```

## Generic Classes

```ts
interface Song {
  title: string;
  artist: string;
}
interface Video {
  title: string;
  creator: string;
  resolution: string;
}
class Playlist<T> {
  public queue: T[] = [];
  add(item: T) {
    this.queue.push(item);
  }
}

const songs = new Playlist<Song>();
```
