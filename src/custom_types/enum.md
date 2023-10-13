# Енумерации

Ключовата дума `enum` позволява създаването на тип, който може да бъде един от няколко различни варианта.
Всеки вариант, който е валиден като `структура`, също е валиден в `enum`.

```rust,editable
// Създаваме `enum` за класифициране на уеб събитие.
// Обърнете внимание как имената и информацията за типа заедно определят варианта:
// `PageLoad != PageUnload` и `KeyPress(char) != Paste(String)`.
// Всеки е различен и независим.
enum WebEvent {
    // Варианта `enum` може да е подобно на `unit`,
    PageLoad,
    PageUnload,
    // като `tuple` структура,
    KeyPress(char),
    Paste(String),
    // или C-подобна структура.
    Click { x: i64, y: i64 },
}

// Функцията приема енумерацията `WebEvent` като аргумент и
// не връща нищо.
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),
        // Деструктурираме `c` от варианта на `enum`.
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),
        // Деструктурираме `Click` в `x` и `y`.
        WebEvent::Click { x, y } => {
            println!("clicked at x={}, y={}.", x, y);
        },
    }
}

fn main() {
    let pressed = WebEvent::KeyPress('x');
    // Функцията `to_owned()` създава отделен `String` от отрязък на низ.
    let pasted  = WebEvent::Paste("my text".to_owned());
    let click   = WebEvent::Click { x: 20, y: 80 };
    let load    = WebEvent::PageLoad;
    let unload  = WebEvent::PageUnload;

    inspect(pressed);
    inspect(pasted);
    inspect(click);
    inspect(load);
    inspect(unload);
}

```

## Псевдоними на типове

Ако използвате псевдоним на тип, можете да се отнасяте към всеки вариант на енум чрез неговия псевдоним.
Това може да бъде полезно, ако името на енума е твърде дълго или твърде общо и искате да го преименувате.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

// Създава псевдоним на типа
type Operations = VeryVerboseEnumOfThingsToDoWithNumbers;

fn main() {
    // Можем да се обръщаме към всяка варианта чрез неговия псевдоним, а не
    // чрез дългото и неудобно име.
    let x = Operations::Add;
}
```

Най-често ще видите това в `impl` блоковете, използвайки псевдонима `Self`.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

impl VeryVerboseEnumOfThingsToDoWithNumbers {
    fn run(&self, x: i32, y: i32) -> i32 {
        match self {
            Self::Add => x + y,
            Self::Subtract => x - y,
        }
    }
}
```

За да научите повече за енуми и псевдоними на типове, можете да прочетете [доклада за стабилизация][aliasreport], когато тази функционалност беше въведена в Rust.

### Вижте също

[`match`][match], [`fn`][fn], и [`String`][str], ["Type alias enum variants" RFC][type_alias_rfc]

[match]: ../flow_control/match.md
[fn]: ../fn.md
[str]: ../std/str.md
[aliasreport]: https://github.com/rust-lang/rust/pull/61682/#issuecomment-502472847
[type_alias_rfc]: https://rust-lang.github.io/rfcs/2338-type-alias-enum-variants.html
