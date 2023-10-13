# Тестов случай: свързан списък

Често срещан начин за имплементиране на свързан списък е чрез `енумерации`:

```rust,editable
use crate::List::*;

enum List {
    // Cons: Tuple структура, която опакова елемент и указател към следващия възел
    Cons(u32, Box<List>),
    // Nil: Възел, който означава края на свързания списък
    Nil,
}

// Методите могат да бъдат прикачени към enum
impl List {
    // Създаваме празен списък
    fn new() -> List {
        // `Nil` е от типа `List`
        Nil
    }

    // Консумираме списъка и връщаме същия списък с нов елемент отпред
    fn prepend(self, elem: u32) -> List {
        // `Cons` също е от типа List
        Cons(elem, Box::new(self))
    }

    // Връщаме дължината на списъка
    fn len(&self) -> u32 {
        // `self` трябва да се съпостави, тъй като поведението на този метод
        // зависи от варианта на `self`
        // `self` е от тип `&List`, и `*self` е от типа `List`, съпоставянето по
        // конкретен тип `T` е предпочитано над съпоставянето чрез референция на`&T`
        // след `Rust 2018` можете да използвате `self` тук и `tail` (без `ref`) по-долу също,
        // rustще извлече типа `&s` и `ref tail`. 
        // Вижте https://doc.rust-lang.org/edition-guide/rust-2018/ownership-and-lifetimes/default-match-bindings.html
        match *self {
            // Не може да се придобие собственост на `tail`, защото `self` е достъпнат;
            // вместо това се взема референция на `tail`
            Cons(_, ref tail) => 1 + tail.len(),
            // Основен случай: Празният списък има дължина нула
            Nil => 0
        }
    }

    // Връщаме представлението на списъка като (разположена в паметта `heap`) низ
    fn stringify(&self) -> String {
        match *self {
            Cons(head, ref tail) => {
                // `format!` е подобно на `print!`, но връща низ разположен в паметта `heap` 
                // вместо да го изпринтира на конзолата
                format!("{}, {}", head, tail.stringify())
            },
            Nil => {
                format!("Nil")
            },
        }
    }
}

fn main() {
    // Създаваме празен свързан списък
    let mut list = List::new();

    // Добавяме няколко елемента
    list = list.prepend(1);
    list = list.prepend(2);
    list = list.prepend(3);

    // Показваме последното състояние на списъка
    println!("linked list has length: {}", list.len());
    println!("{}", list.stringify());
}
```

### Вижте също

[`Box`][box] и [методи][methods]

[box]: ../../std/box.md
[methods]: ../../fn/methods.md
