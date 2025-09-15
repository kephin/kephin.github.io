# Custom Types

## Structures

Three types of `struct` that can be created using the struct keyword:

1. The classic C structs
2. Unit structs, which are field-less, are useful for generics.
3. Tuple structs, which are, basically, named tuples.

```rust
// Define a clissic struct
struct Point {
    x: f32,
    y: f32,
}
// Instantiate a `Point`
let point = Point { x: 5.2, y: 0.4 };
// Make a new point by using struct update syntax
let bottom_right = Point { x: 10.6, ..point }; // { x: 10.6, y: 0.4 }
// Destructure the point using a `let` binding
let Point { x: left_edge, y: top_edge } = point;

// Define a unit struct
struct Unit;
// Instantiate a unit struct
let _unit = Unit;

// Define a tuple struct
struct Pair(i32, f32);
// Instantiate a tuple struct
let pair = Pair(1, 0.1);
```

## Enums

The `enum` keyword allows the creation of a type which may be one of a few different variants. Any variant which is valid as a struct is also valid in an enum.

```rust
enum WebEvent {
    // An `enum` variant may either be Unit-like,
    PageLoad,
    PageUnload,
    // or tuple structs,
    KeyPress(char),
    Paste(String),
    // or c-like structs.
    Click { x: i64, y: i64 },
}

fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),
        // Destructure `c` from inside the `enum` variant.
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),
        // Destructure `Click` into `x` and `y`.
        WebEvent::Click { x, y } => {
            println!("clicked at x={}, y={}.", x, y);
        },
    }
}
```

`enum` can also be used as C-like enums.

```rust
// enum with explicit discriminator
enum Color {
    Red = 0xff0000,
    Green = 0x00ff00,
    Blue = 0x0000ff,
}

fn main() {
    println!("roses are #{:06x}", Color::Red as i32);
    println!("violets are #{:06x}", Color::Blue as i32);
}
```

### Type aliases

```rust
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}
// Creates a type alias
type Operations = VeryVerboseEnumOfThingsToDoWithNumbers;

fn main() {
    let x = Operations::Add;
}
```

### The `use` keyword

`use` declaration can be used so manual scoping isn't needed,

```rust
enum Stage {
    Beginner,
    Advanced,
}

enum Role {
    Student,
    Teacher,
}

fn main() {
    use crate::Stage::{Beginner, Advanced};
    // or automatically `use` each name inside `Role`.
    use crate::Role::*;

    // Equivalent to `Stage::Beginner`.
    let stage = Beginner;
    // Equivalent to `Role::Student`.
    let role = Student;
}
```
