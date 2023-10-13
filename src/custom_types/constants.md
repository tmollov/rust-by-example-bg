# Константи

Rust има два различни типа константи, които могат да бъдат декларирани във всеки обхват
включително глобални. И двете изискват изрична анотация на типа:

* `const`: Непроменлива стойност (общ случай).
* `static`: Възможна мутираща променлива с време за живота [`'static`][static].
  Времето за живот `'static` се извежда и не е необходимо да се посочва.
  Достъпът или модификация на `static` тип променлива е [`несигурно`][unsafe].

```rust,editable,ignore,mdbook-runnable
// Глобалните променливи се декларират извън всеки обхват.
static LANGUAGE: &str = "Rust";
const THRESHOLD: i32 = 10;

fn is_big(n: i32) -> bool {
    // Достъп на константа в някоя функция
    n > THRESHOLD
}

fn main() {
    let n = 16;

    // Достъп на константа в основната нишка
    println!("This is {}", LANGUAGE);
    println!("The threshold is {}", THRESHOLD);
    println!("{} is {}", n, if is_big(n) { "big" } else { "small" });

    // Грешка! Не може да модифицираме `const`.
    THRESHOLD = 5;
    // FIXME ^ Коментирайте този код
}
```

### Вижте също

[The `const`/`static` RFC](
https://github.com/rust-lang/rfcs/blob/master/text/0246-const-vs-static.md),
[`'static` lifetime][static]

[static]: ../scope/lifetime/static_lifetime.md
[unsafe]: ../unsafe.md
