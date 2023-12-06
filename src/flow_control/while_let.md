# while let

Подобно на `if let`, `while let` може да прави can make мъчителните `match` последователности
по-поносими. Помислете за следната последователност, която нараства `i`:

```rust
// Правим `optional` от тип `Option<i32>`
let mut optional = Some(0);

// Опитайте многократно този тест.
loop {
    match optional {
        // Ако `optional` се деструктурира, изпълняваме блока.
        Some(i) => {
            if i > 9 {
                println!("Greater than 9, quit!");
                optional = None;
            } else {
                println!("`i` is `{:?}`. Try again.", i);
                optional = Some(i + 1);
            }
            // ^ Изисква 3 отстъпи!
        },
        // Излезте от цикъла, когато деструктурирането е неуспешно:
        _ => { break; }
        // ^ Защо трябва да се изисква това? Трябва да има по-добър начин!
    }
}
```

Използвайки `while let` прави тази последователност много по-хубава:

```rust,editable
fn main () {
    // Правим `optional` от тип `Option<i32>`
    let mut optional = Some(0);

    // Това се оценавя на: "докато `let` деструктурира `optional` в
    // `Some(i)`, изпълни блока (`{}`). Иначе спри `break`.
    while let Some(i) = optional {
        if i > 9 {
            println!("Greater than 9, quit!");
            optional = None;
        } else {
            println!("`i` is `{:?}`. Try again.", i);
            optional = Some(i + 1);
        }
        // ^ По-малко отклонение надясно и не изисква
        // изрично обработване на неуспешен случай.
    }
    // ^ `if let` имаше допълнителни опции `else`/`else if`
    // клаузи, докато `while let` ги няма.
}
```

### Вижте също

[`enum`][enum], [`Option`][option], и [RFC][while_let_rfc]

[enum]: ../custom_types/enum.md
[option]: ../std/option.md
[while_let_rfc]: https://github.com/rust-lang/rfcs/pull/214
