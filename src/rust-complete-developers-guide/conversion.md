# Conversion

Primitive types can be converted to each other through `casting`.

Rust addresses conversion between custom types (i.e., `struct` and `enum`) by the use of `traits`. The generic conversions will use the `From` and `Into` traits. However there are more specific ones for the more common cases, in particular when converting to and from `Strings`.

## Casting

Rust provides explicit type conversion between primitive types by using the `as` keyword.

```rust,editable
fn main() {
    // number <-> char conversion
    let decimal = 65.4321_f32;
    let integer = decimal as u8;
    println!("decimal converted to integer is : {}", integer); // 65
    let character = integer as char;
    println!("integer converted to character is : {}", character); // 'A'
    // Error! A float cannot be directly converted to a char.
    // let character = decimal as char;

    // signed <-> unsigned conversion
    // For positive numbers, this is the same as the modulus
    println!("1000 as a u8 is : {}", 1000i32 as u8); // 1000 % 256 = 232
    println!(" 232 as a i8 is : {}", 232i32 as i8); // -24
    println!("  -1 as a u8 is : {}", (-1i8) as u8); // 255

    // float -> int conversion
    // when casting from float to int, the `as` keyword performs a *saturating cast*.
    // If the floating point value exceeds the upper bound or is less thane
    // the lower bounds, the returned value will be equal to the bound crossed.
    println!(" 300.0 as u8 is : {}", 300.0_f32 as u8); // 255
    println!("-100.0 as u8 is : {}", -100.0_f32 as u8); // 0
    println!("   nan as u8 is : {}", f32::NAN as u8); // 0
}
```
