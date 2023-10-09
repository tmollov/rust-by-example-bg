# Форматиране

Видяхме, че форматирането се задава чрез *форматиращ низ*:

* `format!("{}", foo)` -> `"3735928559"`
* `format!("0x{:X}", foo)` -> [`"0xDEADBEEF"`][deadbeef]
* `format!("0o{:o}", foo)` -> `"0o33653337357"`

Една и съща променлива (`foo`) може да бъде форматирана различно в зависимост от типа аргумент, който се използва:
`X` или `o`, или *неопределен*.

Тази функционалност за форматиране е имплементирана чрез `trait`-ове, и за всеки тип аргумент има един `trait`.
Най-често използваният сред тях е `Display`, which
който се справя със случаите, когато типът на аргумента не е специфициран: маркера `{}` например.

```rust,editable
use std::fmt::{self, Formatter, Display};

struct City {
    name: &'static str,
    // Latitude - Географска ширина
    lat: f32,
    // Longitude - Географска дължина
    lon: f32,
}

impl Display for City {
    // `f` е буфер, и този метод трябва да запише форматирания низ в него.
    fn fmt(&self, f: &mut Formatter) -> fmt::Result {
        let lat_c = if self.lat >= 0.0 { 'N' } else { 'S' };
        let lon_c = if self.lon >= 0.0 { 'E' } else { 'W' };

        // `write!` е подобно на `format!`, но то ще изпише форматирания низ
        // към буфера (първия аргумент).
        write!(f, "{}: {:.3}°{} {:.3}°{}",
               self.name, self.lat.abs(), lat_c, self.lon.abs(), lon_c)
    }
}

#[derive(Debug)]
struct Color {
    red: u8,
    green: u8,
    blue: u8,
}

fn main() {
    for city in [
        City { name: "Dublin", lat: 53.347778, lon: -6.259722 },
        City { name: "Oslo", lat: 59.95, lon: 10.75 },
        City { name: "Vancouver", lat: 49.25, lon: -123.1 },
    ] {
        println!("{}", city);
    }
    for color in [
        Color { red: 128, green: 255, blue: 90 },
        Color { red: 0, green: 3, blue: 254 },
        Color { red: 0, green: 0, blue: 0 },
    ] {
        // Променете това да използва `{}` когато добавите имплементация
        // за fmt::Display.
        println!("{:?}", color);
    }
}
```

Можете да видите [пълния лист с trait-овете за форматиране][fmt_traits] и техните видове аргументи
в документацията на модула [`std::fmt`][fmt].

### Дейности

Добавете имплементация на `fmt::Display` за структурата `Color` по-горе
така че то се принтира така на конзолата:

```text
RGB (128, 255, 90) 0x80FF5A
RGB (0, 3, 254) 0x0003FE
RGB (0, 0, 0) 0x000000
```

Три съвета, ако закъсате:

* Формулата за изчисляване на цвят в цветовото пространство RGB е:
`RGB = (R*65536)+(G*256)+B , (when R is RED, G is GREEN and B is BLUE)`.
За повече погледнете [RGB color format & calculation][rgb_color].
* Може [да се наложи да изброите всеки цвят повече от веднъж.][named_parameters].
* Можете [да добавите нули с ширина от 2 с форматния спецификатор][fmt_width] със синтаксиса `:0>2`.

### Вижте също

[`std::fmt`][fmt]

[rgb_color]: https://www.rapidtables.com/web/color/RGB_Color.html#rgb-format
[named_parameters]: https://doc.rust-lang.org/std/fmt/#named-parameters
[deadbeef]: https://en.wikipedia.org/wiki/Deadbeef#Magic_debug_values
[fmt]: https://doc.rust-lang.org/std/fmt/
[fmt_traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[fmt_width]: https://doc.rust-lang.org/std/fmt/#width
