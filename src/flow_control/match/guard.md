# Пазачи

*Пазач* на `match` може да се добави, за да се филтрира рамото на съвпадението.

```rust,editable
#[allow(dead_code)]
enum Temperature {
    Celsius(i32),
    Fahrenheit(i32),
}

fn main() {
    let temperature = Temperature::Celsius(35);
    // TODO ^ опитайте различни стойности за `temperature`

    match temperature {
        Temperature::Celsius(t) if t > 30 => println!("{}C is above 30 Celsius", t),
        // Частта с условието `if` ^ е пазачът
        Temperature::Celsius(t) => println!("{}C is below 30 Celsius", t),

        Temperature::Fahrenheit(t) if t > 86 => println!("{}F is above 86 Fahrenheit", t),
        Temperature::Fahrenheit(t) => println!("{}F is below 86 Fahrenheit", t),
    }
}
```

Обърнете внимание, че компилаторът няма да вземе предвид условията на пазачите, когато проверява
дали всички шаблони са обхванати от изразите за съвпаденията.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let number: u8 = 4;

    match number {
        i if i == 0 => println!("Zero"),
        i if i > 0 => println!("Greater than zero"),
        // _ => unreachable!("Should never happen."),
        // TODO ^ разкоментирайте, за да коригирате компилацията
    }
}
```

### Вижте също

[Tuples](../../primitives/tuples.md)
[Енумерации](../../custom_types/enum.md)
