# Деструктуриране на *Tuple*

Различните видове `tuple` могат да бъдат деструктурирани с блока `match` така:

```rust,editable
fn main() {
    let triple = (0, -2, 3);
    // TODO ^ Опитайте различни стойности за `triple`

    println!("Tell me about {:?}", triple);
    // `match` може да бъде използван за деструктурирането на `triple`
    match triple {
        // Деструктуриране на втория и третия елемент
        (0, y, z) => println!("First is `0`, `y` is {:?}, and `z` is {:?}", y, z),
        (1, ..)  => println!("First is `1` and the rest doesn't matter"),
        (.., 2)  => println!("last is `2` and the rest doesn't matter"),
        (3, .., 4)  => println!("First is `3`, last is `4`, and the rest doesn't matter"),
        // `..` може да се използва, за да се игнорира останалата част от дадения `tuple`
        _      => println!("It doesn't matter what they are"),
        // `_` означава да не присвоява стойността в променлива
    }
}
```

### Вижте също

[Tuples](../../../primitives/tuples.md)
