# greenback

Library for safely handling USD values as integers

## Installation

Edit `Cargo.toml`:

```toml
[dependencies]
greenback="0.0.2"
```

## Usage

```rust
extern crate greenback;
use greenback::Greenback;

fn main() {

    // regular arithmetic operations

    let unit_price = Greenback::new(10, 99); // $10.99
    let quantity = 10;
    let coupon = Greenback::new(2, 0); // $2.00 off

    let total_cost = unit_price * quantity - coupon;

    println!("Total cost: {}", total_cost);

    // example 2

    let foo = Greenback::from_float(1.23); // $1.23
    let bar = Greenback::from_cents(4_56); // $4.56
    let baz = Greenback::new(3, 50);       // $3.50

    let sum: Greenback = vec![foo, bar, baz].into_iter().sum();

    if sum > Greenback::zero() {
        println!("sum: {}", sum);
    }
}
```

Output:
```
Total cost: $107.90
sum: $9.29
```

## Status

This is my first Rust package and I'm still learning Rust so user beware!

Pull requests and issues are very welcome.

All the basic arithmetic operations (Add, AddMul, Sub, SubMul, etc.) are implemented along with ordering and summing.  There's also a default formatter which will print your money values like `$1,234.56`.  There's no overflow detection and only limited support for Mul and Div traits.  I need to figure out how to do these using generics properly.