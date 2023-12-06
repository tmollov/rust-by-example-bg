# Деструктуриране на енумерации

Деструктурирането на енумерация (`enum`) става по подобен начин:

```rust,editable
// `allow` се изисква, за да се заглушат предупрежденията, 
// защото е използван само един вариант.
#[allow(dead_code)]
enum Color {
    // Тези трима се определят само от името им.
    Red,
    Blue,
    Green,
    // Също така тези двойки се свързват с `u32`, но с различни имена: видове цветни модели.
    RGB(u32, u32, u32),
    HSV(u32, u32, u32),
    HSL(u32, u32, u32),
    CMY(u32, u32, u32),
    CMYK(u32, u32, u32, u32),
}

fn main() {
    let color = Color::RGB(122, 17, 40);
    // TODO ^ Опитайте различни варианти за `color`

    println!("What color is it?");
    // `enum` може да бъде деструктуриран с помощта на `match`.
    match color {
        Color::Red   => println!("The color is Red!"),
        Color::Blue  => println!("The color is Blue!"),
        Color::Green => println!("The color is Green!"),
        Color::RGB(r, g, b) =>
            println!("Red: {}, green: {}, and blue: {}!", r, g, b),
        Color::HSV(h, s, v) =>
            println!("Hue: {}, saturation: {}, value: {}!", h, s, v),
        Color::HSL(h, s, l) =>
            println!("Hue: {}, saturation: {}, lightness: {}!", h, s, l),
        Color::CMY(c, m, y) =>
            println!("Cyan: {}, magenta: {}, yellow: {}!", c, m, y),
        Color::CMYK(c, m, y, k) =>
            println!("Cyan: {}, magenta: {}, yellow: {}, key (black): {}!",
                c, m, y, k),
        // Нямате нужда от друго рамо, защото всички варианти са разгледани
    }
}
```

### Вижте също

[`#[allow(...)]`][allow], [Цветови модели][color_models] и [Енумерации][enum]

[allow]: ../../../attribute/unused.md
[color_models]: https://bg.wikipedia.org/wiki/%D0%A6%D0%B2%D0%B5%D1%82%D0%BE%D0%B2%D0%B8_%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB
[enum]: ../../../custom_types/enum.md
