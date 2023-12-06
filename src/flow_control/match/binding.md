# Присвояване

Индиректният достъп до променлива прави невъзможно разклоняването и използването на тази променлива без повторното присвояване.
`match` осигурява знака `@` за присвояване на стойности към имена:

```rust,editable
// Функция `age`, която връща `u32`.
fn age() -> u32 {
    15
}

fn main() {
    println!("Tell me what type of person you are");

    match age() {
        0             => println!("I haven't celebrated my first birthday yet"),
        // Можем директно да съпосватим `match` 1 ..= 12, но тогава на колко
        // би било детето? Вместо това, присвояваме го на `n`
        // за последователността от 1 ..= 12. Вече може да се докладва възрастта.
        n @ 1  ..= 12 => println!("I'm a child of age {:?}", n),
        n @ 13 ..= 19 => println!("I'm a teen of age {:?}", n),
        // Нищо не съвпадна. Връщаме резултата.
        n             => println!("I'm an old person of age {:?}", n),
    }
}
```

Можете да използвате "деструктивния" `enum` варианти за присвояване, например `Option`:

```rust,editable
fn some_number() -> Option<u32> {
    Some(42)
}

fn main() {
    match some_number() {
        // Получаваме варианта `Some`, съпоставяме го ако е стойност, и пристояваме го на `n`,
        // което е равно на 42.
        Some(n @ 42) => println!("The Answer: {}!", n),
        // Съпоставяме го какъвто и да е цифра.
        Some(n)      => println!("Not interesting... {}", n),
        // Съпоставяме всичко останало (варианта `None`).
        _            => (),
    }
}
```

### Вижте също

[`Функции`][functions], [`Енумерации`][enums] и [`Option`][option]

[functions]: ../../fn.md
[enums]: ../../custom_types/enum.md
[option]: ../../std/option.md
