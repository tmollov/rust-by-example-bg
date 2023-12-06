# loop

Rust предоставя ключовата дума `loop` за обозначаване на безкраен цикъл.

Изразът `break` може да се използва за излизане от цикъл по всяко време, докато изразът
`continue` може да се използва за пропускане на останалата част от итерацията
и стартиране на нова.

```rust,editable
fn main() {
    let mut count = 0u32;

    println!("Let's count until infinity!");

    // Безкраен цикъл
    loop {
        count += 1;

        if count == 3 {
            println!("three");

            // Пропускаме останалата част от тази итерация
            continue;
        }

        println!("{}", count);

        if count == 5 {
            println!("OK, that's enough");

            // Излизаме от цикъла
            break;
        }
    }
}
```
