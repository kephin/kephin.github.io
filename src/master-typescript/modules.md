# Type Decorations

How to work with 3rd party libraries in TypeScript ecosystem? Check `*.d.ts` file

## Installing Types Separately

For the most part, type declaration packages should always have the same name as the package name on npm, but prefixed with `@types/`.

ref. [TypeScript doc](https://www.typescriptlang.org/docs/handbook/declaration-files/consumption.html)

```bash
npm install --save-dev @types/lodash
```

## Import Types

`import type` only imports declarations to be used for type annotations and declarations. It always gets fully erased, so there’s no remnant of it at runtime. Similarly, export type only provides an export that can be used for type contexts, and is also erased from TypeScript’s output.

```ts
export type { SomeThing };
import type { SomeThing } from "./some-module.js";

// A type-only import can specify a default import or named bindings, but not both.
import type Foo, { Bar, Baz } from "some-module"; // error!
```
