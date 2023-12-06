# Деструктуриране на масиви и отрязъци

Подобно на `tuple`, масивите и отрязъците могат да се деструктурират така:

```rust,editable
fn main() {
    // Опитайте да промените стойностите в масива, или го направете на отрязък!
    let array = [1, -2, 6];

    match array {
        // Присвоете втория и третия елемент в съответни променливи
        [0, second, third] =>
            println!("array[0] = 0, array[1] = {}, array[2] = {}", second, third),

        // Единичните стойности могат да бъдат игнорирани с _
        [1, _, third] => println!(
            "array[0] = 1, array[2] = {} and array[1] was ignored",
            third
        ),

        // Можете също да присвоите някои и да игнорирате останалите
        [-1, second, ..] => println!(
            "array[0] = -1, array[1] = {} and all the other ones were ignored",
            second
        ),
        // Кодът по-долу няма да се компилира
        // [-1, second] => ...

        // или ги запазете в друг масив/отрязък
        // (типът зависи от този на стойността, срещу която се съпоставя)
        [3, second, tail @ ..] => println!(
            "array[0] = 3, array[1] = {} and the other elements were {:?}",
            second, tail
        ),

        // С комбинирането на тези шаблони, например, можем да присвояваме първата
        // и последната стойност, и да ги съхраним останалите в един масив
        [first, middle @ .., last] => println!(
            "array[0] = {}, middle = {:?}, array[2] = {}",
            first, middle, last
        ),
    }
}
```

### Вижте също

[Масиви и отрязъци](../../../primitives/array.md) и [Binding](../binding.md) for `@` sigil
