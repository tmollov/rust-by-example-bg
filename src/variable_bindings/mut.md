# Изменчивост - мутабилност

Променливите по подразбиране са неизменяеми (immutable - не могат да мутират), но това може да бъде заменено с `mut` модификатора.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let _immutable_binding = 1;
    let mut mutable_binding = 1;

    println!("Before mutation: {}", mutable_binding);

    // ОК
    mutable_binding += 1;

    println!("After mutation: {}", mutable_binding);

    // Грешка! Не може да се присвои нова стойност на неизменяема променлива.
    _immutable_binding += 1;
}
```

Компилаторът ще генерира подробно съобщение за грешка относно проблеми с мутабилността.
