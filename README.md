# ab5-logging

A small Rust library for printing multi-line text with smooth RGB color gradients in the terminal using ANSI 24-bit color escape codes.

## Features

- **Horizontal gradients** — color shifts left-to-right across each line
- **Vertical gradients** — color shifts top-to-bottom across lines
- **Zero dependencies** — pure Rust, no external crates

## Requirements

- Rust 2021 edition or later
- A terminal that supports 24-bit (true color) ANSI escape sequences

## Installation

Add this crate to your `Cargo.toml`:

```toml
[dependencies]
ab5-logging = { path = "path/to/ab5-logging" }
```

Or, once published to crates.io:

```toml
[dependencies]
ab5-logging = "0.1"
```

## Usage

```rust
use ab5_logging::{horizontal, vertical};

fn main() {
    let text = "Hello\nWorld";

    // Red (255, 0, 0) → Blue (0, 0, 255), gradient across each line
    horizontal(255, 0, 0, 0, 0, 255, text);

    // Same colors, gradient from line to line
    vertical(255, 0, 0, 0, 0, 255, text);
}
```

## API

### `horizontal`

```rust
pub fn horizontal(
    start_red: u8, start_green: u8, start_blue: u8,
    end_red: u8, end_green: u8, end_blue: u8,
    text: &str,
)
```

Prints `text` with a horizontal RGB gradient. On each line, the color interpolates from the start color to the end color based on character position. The gradient resets at the beginning of each new line.

### `vertical`

```rust
pub fn vertical(
    start_red: u8, start_green: u8, start_blue: u8,
    end_red: u8, end_green: u8, end_blue: u8,
    text: &str,
)
```

Prints `text` with a vertical RGB gradient. Each line uses a single color, and the color interpolates from the start color on the first line to the end color on the last line.

Both functions reset terminal styling with `\x1b[0m` after printing.

## Development

```bash
# Run tests (prints gradient samples to stdout)
cargo test

# Build the library
cargo build
```

## License

No license file is included yet. Check the repository for updates.
