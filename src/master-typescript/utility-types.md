# Utility Types

## Partial

Constructs a type with all properties of Type set to `optional`.

```ts
interface Course {
  title: string;
  length: number;
}
const updateCourse = (id: string, course: Partial<Course>) => {
  // ...
};
updateCourse("123", {
  title: "Typescript",
});
```

## Pick

Constructs a type by picking the set of properties Keys (string literal or union of string literals) from Type.

```ts
interface Todo {
  title: string;
  description: string;
  completed: boolean;
  createdAt: number;
}

type TodoPreview = Pick<Todo, "title" | "completed">;

const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
};
```

## Omit

The opposite of `Pick`.

```ts
type TodoInfo = Omit<Todo, "completed" | "createdAt">;

const todoInfo: TodoInfo = {
  title: "Pick up kids",
  description: "Kindergarten closes at 5pm",
};
```
