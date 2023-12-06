# Вложени и етикетирани

Възможно е да използвате `break` или `continue` във външните цикли, когато работите с вложени такива.
В тези случаи циклите трябва да бъдат анотирани с някакъв етикет с формат: `'име-на-етикета`,
и етикета трябва да се подаде на изразите `break`/`continue`.

```rust,editable
#![allow(unreachable_code, unused_labels)]

fn main() {
    'outer: loop {
        println!("Entered the outer loop");

        // Етикет с име `inner`
        'inner: loop {
            println!("Entered the inner loop");

            // Това ще прекъсне само вътрешния цикъл
            //break;

            // Това ще прекъсва външния цикъл
            break 'outer;
        }

        println!("This point will never be reached");
    }

    println!("Exited the outer loop");
}
```
