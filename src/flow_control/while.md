# while

Ключовата дума `while` може да се използва за изпълнение на цикъл, докато дадено условие е вярно.

Нека напишем прословутия [FizzBuzz][fizzbuzz] с помощта на цикъла `while`.

```rust,editable
fn main() {
    // Брояч
    let mut n = 1;

    // Циклим докато `n` е по малко от 101
    while n < 101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }

        // Увеличаваме брояча
        n += 1;
    }
}
```

[fizzbuzz]: https://en.wikipedia.org/wiki/Fizz_buzz
