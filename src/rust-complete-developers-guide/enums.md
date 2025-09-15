# Enums: Unleashed Pattern Matching and Options

When we need to modal several different things that are all kind of similar, two options for this:

1. `Structs`
2. `Enums`

Defining enums,

```rust
// Book, Movie, AudioBook, Podcast and Placeholder are all of the type Media
// We can define functions accept values of type 'Media'
#[derive(Debug)]
enum Media {
    Book { title: String, author: String },
    Movie { title: String, director: String },
    AudioBook { title: String },
    Podcast(u32), // unlabeled field
    Placeholder, // no field
}

fn print_media(media: Media) {
    println!("{:#?}", media);
}
fn main() {
    let book = Media::Book {
        title: String::from("A book."),
        author: String::from("An author")
    };
    let movie = Media::Movie {
        title: String::from("A movie."),
        director: String::from("A director")
    };
    let audio_book = Media::AudioBook {
        title: String::from("An audiobook."),
    };
    let podcast = Media::Podcast(1);
    let placeholder = Media::Placeholder;

    print_media(book);
    print_media(movie);
    print_media(audio_book);
    print_media(podcast);
    print_media(placeholder);
}
```

## Adding Implementations to Enums

Let's say we want to add a method `description` under `Media` enum, there are two ways to do type checking,

1. pattern matching, `if let ...`
2. `match` statement -> suggested

```rust
#[derive(Debug)]
enum Media { /* */ }
impl Media {
    // 1. Pattern Matching
    fn description(&self) -> String {
        if let Media::Book { title, author } = self {
            format!("Book: {} {}", title, author)
        } else if let Media::Movie { title, director } = self {
            format!("Movie: {} {}", title, director)
        } else if let Media::AudioBook { title } = self {
            format!("Audio Book: {}", title)
        } else if let Media::Podcast(id) = self {
            format!("Podcast: {}", id)
        } else if let Media::Placeholder = self {
            format!("Placeholder")
        } else {
            String::from("Media description")
        }
    }
    // 2. `match` statement
    fn description(&self) -> String {
        match self {
            Media::Book { title, author } => format!("Book: {} {}", title, author),
            Media::Movie { title, director } => format!("Movie: {} {}", title, director),
            Media::AudioBook { title } => format!("Audio Book: {}", title),
            Media::Podcast(id) => format!("Podcast: {}", id),
            Media::Placeholder => format!("Placeholder"),
        }
}

fn main() {
    let book = Media::Book { /* */ };
    let movie = Media::Movie { /* */ };
    let audio_book = Media::AudioBook { /* */ };
    let podcast = Media::Podcast(1);
    let placeholder = Media::Placeholder;

    println!("{}", book.description());
    println!("{}", movie.description());
    println!("{}", audio_book.description());
    println!("{}", podcast.description());
    println!("{}", placeholder.description());
}
```

Deciding when to use `enums` v.s `structs`, ask one question:

- Does each thing you're modeling have the **same methods**? -> use `enums`
- Does each thing have some same, some different methods? -> use `structs`

## The Option Enum

```rust
enum Option {
    Some(value),
    None,
}
```

- Rust doesn't have `null`, `nil` or `undefined`.
- Instead, we get a built-in enum `Option` having two variants: `Some` and `None`.
- This forces us to handle and avoid unexpected errors.

For example, when we want to get an item from a list,

```rust
// 'match' statement
match vec![1, 2, 3].get(10) {
    Some(value) => println!("Value: {}", value),
    None => println!("Nothing at the index"),
}

// pattern matching
if let Some(value) = vec![1, 2, 3].get(0) {
    println!("Value: {}", value)
} else {
    println!("Nothing at the index")
}
```

Using `match` is the ideal way to figure out if we have `Some` or `None`, but there are other ways that are more compact but have big downsides.

1. `item.unwrap()`
   - if item is `Some`, returns the value in the `Some`
   - if item is `None`, panics!
   - use for quick debugging
2. `item.expect("there should be a value here")`
   - if item is `Some`, returns the value in the `Some`
   - if item is `None`, prints the provided debug message and panics!
   - use when we **want** to crash if there is no value
3. `item.unwrap_or(&placeholder)`
   - if item is `Some`, returns the value in the `Some`
   - if item is `None`, returns the provided value
   - use when it makes sense to provide a fallback value


