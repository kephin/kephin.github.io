# Working with DOM

TypeScript knows about the `document`.

```ts
const element = document.getElementById("test");
```

## Non-null assertion operators

Put the `!` behind means it's not null.

```ts
const btn = document.getElementById("btn")!;
btn.addEventListener("click", () => {
  console.log("clicked!");
});
```

## Type assertions

We can tell TypeScript what is the type of this value by the `as` keyword.

```ts
const mystery: unknown = "my name";
const numChars = (mystery as string).length;

// HTMLElement doesn't have 'value' property
// we need to tell TypeScript it's the HTMLInputElement
const input = document.getElementById("input")! as HTMLInputElement;
console.log(input.value);

// there's another way, but be aware, this syntax doesn't work with jsx
const input = document.getElementById("input");
console.log((<HTMLInputElement>input).value);
```

## Working with Event

```ts
const form = document.querySelector("form")!;

// #1. TS doesn't know what evt is, so we have to add type annotation
const handleSubmit = (evt: SubmitEvent) => {
  evt.preventDefault();
};
form.addEventListener("click", handleSubmit);

// #2. TS knows evt is SubmitEvent if we define the function inline
form.addEventListener("click", (evt) => {
  evt.preventDefault();
});
```
