# Variable Bindings

## Mutability

Variable bindings are immutable by default, but this can be overridden using the `mut` modifier.

```rust
fn main() {
    let immutable_binding = 1;
    let mut mutable_binding = 1;

    // Ok
    mutable_binding += 1;
}
```

## Scope and Shadowing

1. Variable bindings have a scope, and are constrained to live in a block `{}`.
2. Variable _shadowing_ is allowed.

```rust
fn main () {
    let long_lived_binding = 1;

    // smaller scope
    {
        // this binding only exists in this block
        let short_lived_binding = 2;

        // this binding can *shadow* the outer one
        let long_lived_binding = "abc";
        println!("{}", long_lived_binding); // abc

    }
    println!("{}", short_lived_binding); // Error! `short_lived_binding` doesn't exist in this scope

    // this binding *shadows* the previous binding
    let long_lived_binding = 3;
    println!("{}", long_lived_binding); // 3
}
```
