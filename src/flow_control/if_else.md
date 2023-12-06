# if/else

Разклоняването с `if`-`else` е подобно на другите езици. За разлика от много от тях,
булевото условие не се нуждае от скоби, и след всяко условие следва блок. `if`-`else`  условията са изрази,
и всички клонове трябва да връщат същия тип.

```rust,editable
fn main() {
    let n = 5;

    if n < 0 {
        print!("{} is negative", n);
    } else if n > 0 {
        print!("{} is positive", n);
    } else {
        print!("{} is zero", n);
    }

    let big_n =
        if n < 10 && n > -10 {
            println!(", and is a small number, increase ten-fold");

            // Този израз връща `i32`.
            10 * n
        } else {
            println!(", and is a big number, halve the number");

            // Този израз също трябва да връща `i32`.
            n / 2
            // TODO ^ Опитайте да потиснете този израз с точка и запетая.
        };
    //   ^ Не забравяйте да поставите точка и запетая тук! Всички `let` изрази изискват това.

    println!("{} -> {}", n, big_n);
}
```
