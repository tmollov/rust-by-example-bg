# Обхват и презаписване

Променливите имат област на валидност и са ограничени да съществуват в рамките на *блок* (block).
Блокът представлява колекция от конструкции, затворени в скоби `{}`.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Тази променлива живее в основната функция
    let long_lived_binding = 1;

    // Това е блок и има по-малък обхват от основната функция
    {
        // Тази променлива съществува само в този блок
        let short_lived_binding = 2;

        println!("inner short: {}", short_lived_binding);
    }
    // Край на блока

    // Грешка! `short_lived_binding` не съществува в този обхват
    println!("outer short: {}", short_lived_binding);
    // FIXME ^ Коментирайте този ред

    println!("outer long: {}", long_lived_binding);
}
```

Също така, [презаписването на променливи][variable-shadow] е позволено.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let shadowed_binding = 1;

    {
        println!("before being shadowed: {}", shadowed_binding);

        // Тази променлива *презаписва* външното
        let shadowed_binding = "abc";

        println!("shadowed in inner block: {}", shadowed_binding);
    }
    println!("outside inner block: {}", shadowed_binding);

    // Тази променлива *презаписва* предишната променлива
    let shadowed_binding = 2;
    println!("shadowed in outer block: {}", shadowed_binding);
}
```

[variable-shadow]: https://en.wikipedia.org/wiki/Variable_shadowing
