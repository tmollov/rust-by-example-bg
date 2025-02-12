# Литерали

Числовите литерали могат да бъдат анотирани с тип, като се добави суфикс след литерала. Например,
за да укажете, че литералът `42` трябва да има тип `i32`, можете на напишете `42i32`.

Типът на числовите литерали без суфикс ще зависи от това как се използват.
Ако няма ограничение, компилаторът ще използва `i32` за целочислени числа
и `f64` за числа с плаваща запетая.

```rust,editable
fn main() {
    // Суфиксирани литерали - техните типове се знаят при инициализацията.
    let x = 1u8;
    let y = 2u32;
    let z = 3f32;

    // Литерали без суфикс - техните типове зависят от начина, по който се използват.
    let i = 1;
    let f = 1.0;

    // `size_of_val` връща размера на променливите в байтове
    println!("size of `x` in bytes: {}", std::mem::size_of_val(&x));
    println!("size of `y` in bytes: {}", std::mem::size_of_val(&y));
    println!("size of `z` in bytes: {}", std::mem::size_of_val(&z));
    println!("size of `i` in bytes: {}", std::mem::size_of_val(&i));
    println!("size of `f` in bytes: {}", std::mem::size_of_val(&f));
}
```

В предишния код са използвани някои концепции, които още не са обяснени.
Ето кратко обяснение за нетърпеливите читатели:

* `std::mem::size_of_val` е функция, но е извикат чрез "пълния път".
  Кодът може да бъде разделен на логически единици, наречени *модули*. В този случай,
  функцията `size_of_val` е дефинирана в модула `mem`, а модулът `mem`
  е дефиниран в *пакета (crate)* `std`. За повече подробности, вижте
  [модули][mod] и [пакети][crate].

[mod]: ../mod.md
[crate]: ../crates.md
