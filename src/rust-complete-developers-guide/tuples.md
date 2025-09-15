# Introduce Tuples

```rust
type Rgb = (u8, u8, u8);
fn make_rgb() -> Rgb {
    (0, 128, 255)
}

fn main() {
    let color = make_rgb();
    let red = color.0;
}
```
