# Handling the Unexpected Errors and Results

Introducing the `Result` enum,

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

## Type of Errors

- Many modules in the std lib have their own custom error types
  - `std::str::Utf8Error`
  - `std::string::FromUtf8Error`
  - `std::num::ParseIntError`
  - `std::num::ParseFloatError`
  - `std::num::TryFromIntError`
  - `std::thread::JoinError`
  - `std::io::Error`
- You can also create your own custom types of errors
- There is no general-purpose catch-all type of error, like `Error` in JavaScript or `Exception` in Python

```rust
// Import and used to represent an error
use std::io::Error;

fn divide(a: f64, b: f64) -> Result<f64, Error> {
    if b == 0.0 {
        Err(Error::other("can't divided by 0")) // Create an instance of the Error
    } else {
        Ok(a / b)
    }
}

fn main() {
    match divide(5.0, 3.0) {
        // The calculated value is 1.66667
        Ok(value) => println!("The calculated value is {:#?}", value),

        // Custom { kind: Other, error: "can't divided by 0" }
        Err(err) => println!("{:#?}", err),
    }
}
```

## Empty Ok Variants

Consider if we have a successful operation that does not give us any value,

- writing data to a file
- removing a file/directory
- permission check
- validating a string

Since `Ok` variant must have something inside it, we pass empty tuple -> `Ok(())`.

Then inside the `match` statement, we use `..` if we want to ignore the values inside the `Ok` variant.

```rust
fn validating_email(email: String) -> Result<(), Error> {
    if email.contains('@') {
        // pass empty tuple
        Ok(())
    } else {
        Err(Error::other("email must have an @"))
    }
}

fn main() {
    match validating_email(String::from("test@test.com")) {
        // to ignore values inside the Ok variant
        Ok(..) => println!("email is valid!"),
        Err(err) => println!("{}", err)
    }
}
```

