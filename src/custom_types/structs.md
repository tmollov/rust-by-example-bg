# Структури

Има три типа структури, които могат да бъдат създадени чрез ключовата дума `struct`:

* Tuple структури, които са, по същество, именовани тупъли.
* Класическата [структури от езика "C"][c_struct]
* Unit структури, които нямат полета, са полезни за генерици.

```rust,editable
// Атрибут, който скрива предупрежденията за неползван код.
#![allow(dead_code)]

#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}

// Структура Unit
struct Unit;

// Структура Tuple
struct Pair(i32, f32);

// Структура с две полета
struct Point {
    x: f32,
    y: f32,
}

// Структурите могат да бъдат преизползвани от други структури
struct Rectangle {
    // Правоъгълник може да бъде определен чрез позицията на
    // горния ляв и долния десен ъгъл в двуизмерното пространството.
    top_left: Point,
    bottom_right: Point,
}

fn main() {
    // Създай структура със съкратена инициализация на полетата
    let name = String::from("Peter");
    let age = 27;
    let peter = Person { name, age };

    // Принтирайте структурате с `debug` маркера
    println!("{:?}", peter);

    // Създайте инстанция на `Point`
    let point: Point = Point { x: 10.3, y: 0.4 };

    // Осъществете достъп до полетата на точката
    println!("point coordinates: ({}, {})", point.x, point.y);

    // Създай нова точка, като използваш синтаксиса за обновяване на структурата, 
    // за да използваш полетата на нашата предишна точка
    let bottom_right = Point { x: 5.2, ..point };

    // `bottom_right.y` ще е същото като `point.y`, защото използвахме полето
    // от `point`
    println!("second point: ({}, {})", bottom_right.x, bottom_right.y);

    // Разгради точката, използвайки `let`
    let Point { x: left_edge, y: top_edge } = point;

    let _rectangle = Rectangle {
        // инстанцирането на структура също е израз
        top_left: Point { x: left_edge, y: top_edge },
        bottom_right: bottom_right,
    };

    // Създаване на `Unit` структура
    let _unit = Unit;

    // Създаване на `Tuple` структура
    let pair = Pair(1, 0.1);

    // Достъп до полетата на `Tuple` структурата
    println!("pair contains {:?} and {:?}", pair.0, pair.1);

    // Деструктуриране на `Tuple` структурата
    let Pair(integer, decimal) = pair;

    println!("pair contains {:?} and {:?}", integer, decimal);
}
```

### Упражнения

1. Добавете функция `rect_area`, която изчислява площа на `Rectangle` (използвайте вложени деструктурирания).
2. Добавете функция `square`, която приема `Point` и `f32` като аргументи,
   и връща `Rectangle`, с което горния-ляв ъгъл е точка(`Point`), а дължината и височината му съответстват на `f32`.

### Вижте също

[`атрибути`][attributes], и [деструктуриране][destructuring]

[attributes]: ../attribute.md
[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[destructuring]: ../flow_control/match/destructuring.md
