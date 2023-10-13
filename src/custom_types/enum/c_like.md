# C-подобни

`enum` може също да е подобно на енумите в C езика: C-подобно.

```rust,editable
// Атрибут, който скрива предупрежденията за неползван код.
#![allow(dead_code)]

// Енумерация с неясен дискриминатор (стартира от 0)
enum Number {
    Zero,
    One,
    Two,
}

// Енумерация с ясен дискриминатор
enum Color {
    Red = 0xff0000,
    Green = 0x00ff00,
    Blue = 0x0000ff,
}

fn main() {
    // `enums` могат да бъдат cast-нати (превръщани) като цели числа.
    println!("zero is {}", Number::Zero as i32);
    println!("one is {}", Number::One as i32);

    println!("roses are #{:06x}", Color::Red as i32);
    println!("violets are #{:06x}", Color::Blue as i32);
}
```

### Вижте също

[casting][cast]

[cast]: ../../types/cast.md
