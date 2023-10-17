# В или от тип String

## Конвертиране в String

За да конвертирате всякакъв тип в `String`, просто трябва да имплементирате [`ToString`]
за този тип. По-добре е да имплементирате [`fmt::Display`][Display],
което автоматично предоставя и [`ToString`] и ви позволява да отпечатвате стойността на типа,
както беше обяснено в раздела за [`print!`][print].

```rust,editable
use std::fmt;

struct Circle {
    radius: i32
}

impl fmt::Display for Circle {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "Circle of radius {}", self.radius)
    }
}

fn main() {
    let circle = Circle { radius: 6 };
    println!("{}", circle.to_string());
}
```

## Парсване на String

Едно от по-честите преобразувания е от низ към число. Идиоматичният начин за това е
да използвате функцията [`parse`] и след това или да оставите на инферентността на типа
или да указвате типа, който ще се парсне, използвайки синтаксиса с 'turbofish' синтаксиса.
И двете алтернативи са показани в следния пример.

Това ще преобразува низа в типа, указан в скобите, докато е имплементиран [`FromStr`] за този тип.
[`FromStr`] е имплементиран за множество типове в стандартната библиотека.
За да получите тази функционалност за потребителски дефиниран тип,
просто имплементирайте [`FromStr`] за този тип.

```rust,editable
fn main() {
    let parsed: i32 = "5".parse().unwrap();
    let turbo_parsed = "10".parse::<i32>().unwrap();

    let sum = parsed + turbo_parsed;
    println!("Sum: {:?}", sum);
}
```

[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[Display]: https://doc.rust-lang.org/std/fmt/trait.Display.html
[print]: ../hello/print.md
[`parse`]: https://doc.rust-lang.org/std/primitive.str.html#method.parse
[`FromStr`]: https://doc.rust-lang.org/std/str/trait.FromStr.html
