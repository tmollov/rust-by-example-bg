# Debug

Всички типове, които искат да използват форматиращите трейтове от `std::fmt`, изискват имплементация, за да могат да бъдат изведени. Автоматични имплементации се предоставят само за типове като тези в библиотеката **std**. Всички останали **трябва** да бъдат ръчно имплементирани по някакъв начин.

Трейта `fmt::Debug` го прави много ясно и лесно за разбиране. *Всички* типове могат, с атрибута
`derive`, автоматично да създадат имплементация на `fmt::Debug`.
Това не важи за `fmt::Display`, която трябва да се имплементира ръчно.

```rust
// Тази структура не може да бъде изведена нито с `fmt::Display`,
// нито с `fmt::Debug`.
struct UnPrintable(i32);

// Атрибута `derive` автоматично създава необходимата имплементация,
// за да направи тази структура изпечатваемa с `fmt::Debug`.
#[derive(Debug)]
struct DebugPrintable(i32);
```

Всички типове от стандартната библиотека `std` също се принтират автоматично с `{:?}`:

```rust,editable
// Наследяваме `fmt::Debug` имплементация за типа `Structure`. 
// `Structure` е структура, което съдържа единствено `i32`.
#[derive(Debug)]
struct Structure(i32);

// Подаваме `Structure` на структурата `Deep`. 
// Това го прави изпечатваем също.
#[derive(Debug)]
struct Deep(Structure);

fn main() {
    // Принтирането с `{:?}` е подобно на `{}`.
    println!("{:?} months in a year.", 12);
    println!("{1:?} {0:?} is the {actor:?} name.",
             "Slater",
             "Christian",
             actor="actor's");

    // `Structure` е изпечатваема!
    println!("Now {:?} will print!", Structure(3));

    // Проблема с атрибута `derive` е че нямаме контрол върху това как ще изглежда резултатът.
    // Какво бихме направили, ако искаме да се показва само '7' ?
    println!("Now {:?} will print!", Deep(Structure(7)));
}
```

И така, `fmt::Debug` определено прави това изпечатваемо, но жертва малко елегантност.
Rust също предоставя "красиво принтиране" с `{:#?}`.

```rust,editable
#[derive(Debug)]
struct Person<'a> {
    name: &'a str,
    age: u8
}

fn main() {
    let name = "Peter";
    let age = 27;
    let peter = Person { name, age };

    // "Красиво принтиране"
    println!("{:#?}", peter);
}
```

Можете ръчно да имплементирате `fmt::Display`, за да контролирате извеждането при принтиране.

### Вижте също

[`attributes`][attributes], [`derive`][derive], [`std::fmt`][fmt],
и [`struct`][structs]

[attributes]: https://doc.rust-lang.org/reference/attributes.html
[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[structs]: ../../custom_types/structs.md
