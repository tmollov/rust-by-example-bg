# Display

`fmt::Debug` не изглежда компактно и чисто, затова персонализирането на изхода често е.
Това се постига чрез ръчна имплементация на
[`fmt::Display`][fmt], която използва маркера `{}`.
Имплементацията изглежда по следния начин:

```rust
// Импортирайте (чрез `use`) модула `fmt`, за да го направите достъпен.
use std::fmt;

// Дефинирайте структура, за която ще бъде имплементирано `fmt::Display`. 
// Това е структура от тип 'tuple' с име `Structure`, което съдържа цяло число `i32`.
struct Structure(i32);

// За да се използва маркера `{}`, трябва да се имплементира ръчно trait-а `fmt::Display` за типа.
impl fmt::Display for Structure {
    // Този trait изисква `fmt` с точно тази сигнатура.
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        
        // Записва стриктно първия елемент в предоставения изходен поток: `f`.
        // Връща `fmt::Result`, който показва дали операцията е успешна или не. 
        // Забележете, че  `write!` използва синтаксис, който е много подобен на `println!`.
        write!(f, "{}", self.0)
    }
}
```

`fmt::Display` може да е по-ясен от `fmt::Debug`, но това представлява проблем за стандартната библиотека `std`.
Как трябва да се показват двусмислените типове?
Например, ако стандартната библиотека `std` имплементира един стил за всички `Vec<T>`, какъв стил трябва да е то? Дали ще бъде някое от тези двете?

* `Vec<path>`: `/:/etc:/home/username:/bin` (split on `:`)
* `Vec<number>`: `1,2,3` (split on `,`)

Не, защото няма идеален стил за всички типове и библиотеката `std` не предполага да налага такъв. `fmt::Display` не е имплементиран за `Vec<T>`
или за други `generics` контейнери. Затова за тези обобщени случаи трябва да се използва  `fmt::Debug`.

Обаче този проблем не се появява, тъй като всеки нов контейнер, който **не е** от тип `generics`,  може да бъде имплементира `fmt::Display`.

```rust,editable
use std::fmt; // Импортиране на модула `fmt`

// Структура, която съдържа две числа. 
// `Debug` ще бъде автоматично извлечена, така че резултатите могат да се сравняват с`Display`.
#[derive(Debug)]
struct MinMax(i64, i64);

// Имплементация на `Display` за `MinMax`.
impl fmt::Display for MinMax {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Използваме `self.`, за да реферираме към точките от данни.
        write!(f, "({}, {})", self.0, self.1)
    }
}

// Дефиниция на структура, където полетата са наименовани за съпоставка.
#[derive(Debug)]
struct Point2D {
    x: f64,
    y: f64,
}

// Аналогично, имплементация на `Display` за `Point2D`.
impl fmt::Display for Point2D {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Персонализиране, така че да се принтират само `x` и `y`.
        write!(f, "x: {}, y: {}", self.x, self.y)
    }
}

fn main() {
    let minmax = MinMax(0, 14);

    println!("Compare structures:");
    println!("Display: {}", minmax);
    println!("Debug: {:?}", minmax);

    let big_range =   MinMax(-300, 300);
    let small_range = MinMax(-3, 3);

    println!("The big range is {big} and the small is {small}",
             small = small_range,
             big = big_range);

    let point = Point2D { x: 3.3, y: 7.2 };

    println!("Compare points:");
    println!("Display: {}", point);
    println!("Debug: {:?}", point);

    // Грешка. `Debug` и `Display` са имплементирани, но маркера `{:b}`
    // изисква `fmt::Binary` да е имплементирано. Това няма да проработи.
    // println!("What does Point2D look like in binary: {:b}?", point);
}
```

Така че, `fmt::Display` бе имплементирано, но `fmt::Binary` не, и затова не може да се изпозлва.
`std::fmt` има много [`traits`][traits] и всяка от тях изискват and всеки изисква
собствена имплементация. Това е описано подробно по-нататък в [`std::fmt`][fmt].

### Упражнения

След като проверите резултата от горния пример, използвайте структурата `Point2D` като a
ръководство за добавяне на структура `Complex` към примера. При отпечатване със същия
начин, изходът трябва да бъде:

```txt
Display: 3.3 + 7.2i
Debug: Complex { real: 3.3, imag: 7.2 }
```

### Вижте също

[`derive`][derive], [`std::fmt`][fmt], [`macros`][macros], [`struct`][structs],
[`trait`][traits], и [`use`][use]

[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../../macros.md
[structs]: ../../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[use]: ../../mod/use.md
