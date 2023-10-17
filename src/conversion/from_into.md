# `From` и `Into`

[`From`] и [`Into`] са в същност взаимно свързани и това е фактически част от тяхната имплементация.
Ако имате възможност да конвертирате тип A от тип B, тогава би трябвало лесно да се предположи,
че трябва да бъде възможно и конвертирането на тип B към тип A.

## `From`

The [`From`] позволява на даден тип да дефинира как да се създаде от друг тип,
предоставяйки този начин за конвертиране между различни типове.
В стандартната библиотека има множество имплементации на този `trait`,
които позволяват конвертиране между примитивни и общо използвани типове.

Например много лесно можем да конвертираме `str` в `String`

```rust
let my_str = "hello";
let my_string = String::from(my_str);
```

Подобно на това, можем да дефинираме конверсия за нашия собствен тип.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Number {
    value: i32,
}

impl From<i32> for Number {
    fn from(item: i32) -> Self {
        Number { value: item }
    }
}

fn main() {
    let num = Number::from(30);
    println!("My number is {:?}", num);
}
```

## `Into`

[`Into`] е просто обратното на `From`. Това означава, че ако сте имплементирали `From` за вашия тип,
`Into` ще го извиква, когато е необходимо.

Използването на `Into` обикновено изисква указване на типа, към който да се конвертира,
тъй като компилаторът не може да го определи в повечето случаи.
Въпреки това, това е малък компромис, тъй като получаваме функционалността безплатно.

```rust,editable
use std::convert::Into;

#[derive(Debug)]
struct Number {
    value: i32,
}

impl Into<Number> for i32 {
    fn into(self) -> Number {
        Number { value: self }
    }
}

fn main() {
    let int = 5;
    // Опитайте да премахнете анотацията за типа
    let num: Number = int.into();
    println!("My number is {:?}", num);
}
```

[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html
