# if let

За някои случаи при съпоставяне на енумерации, match е неудобен. Например:

```rust
// Направете 'optional' от тип Option<i32>
let optional = Some(7);

match optional {
    Some(i) => {
        println!("This is a really long string and `{:?}`", i);
        // ^ Необходими са 2 вдлъбнатини, просто за да можем да деструктурираме
        // `i` от опцията.
    },
    _ => {},
    // ^ Необходимо е, защото `match` е изчерпателен. Не изглежда ли
    // като изгубено пространство?
};

```

`if let` по-четлив за този случай и допълнително позволява
да се указват различни опции за неуспех:

```rust,editable
fn main() {
    // Всичките са от тип `Option<i32>`
    let number = Some(7);
    let letter: Option<i32> = None;
    let emoticon: Option<i32> = None;

    // Конструкцията `if let` чете: "ако `let` деструктурира `number` в
    // `Some(i)`, изпълни блока (`{}`).
    if let Some(i) = number {
        println!("Matched {:?}!", i);
    }

    // Ако трябва да укажете грешка, използвайте else:
    if let Some(i) = letter {
        println!("Matched {:?}!", i);
    } else {
        // Деструктурирането се провали. Минаваме на неуспешния скучай.
        println!("Didn't match a number. Let's go with a letter!");
    }

    // Предоставете променено условие за неуспех.
    let i_like_letters = false;

    if let Some(i) = emoticon {
        println!("Matched {:?}!", i);
    // Деструктурирането се провали. Оценете условието `else if`, за да видите дали
    // трябва да се вземе алтернативен неуспешен клон:
    } else if i_like_letters {
        println!("Didn't match a number. Let's go with a letter!");
    } else {
        // Условието е оценено като грешно. Този клон е по подразбиране:
        println!("I don't like letters. Let's go with an emoticon :)!");
    }
}
```

По същия начин, `if let` може да се използва за съпоставяне на всякакви стойности на **enum**:

```rust,editable
// Примерният ни enum
enum Foo {
    Bar,
    Baz,
    Qux(u32)
}

fn main() {
    // Създайте примерни променливи
    let a = Foo::Bar;
    let b = Foo::Baz;
    let c = Foo::Qux(100);
    
    // Проверяваме дали променливата 'a' съвпада с Foo::Bar
    if let Foo::Bar = a {
        println!("a is foobar");
    }
    
    // Променливата 'b' не съответства на Foo::Bar
    // Така че това няма да отпечата нищо
    if let Foo::Bar = b {
        println!("b is foobar");
    }
    
    // Променливата 'c' съответства на Foo::Qux, което има стойност
    // подобен на 'Some()' като в предишния ни пример
    if let Foo::Qux(value) = c {
        println!("c is {}", value);
    }

    // Присвояването също работи с `if let`
    if let Foo::Qux(value @ 100) = c {
        println!("c is one hundred");
    }
}
```

Друга полза е, че `if let` ни позволява да съпоставим непараметризирани варианти на enum. Това е вярно дори в случаите, когато enum не имплементира или наследява `PartialEq`. При такива случаи `if Foo::Bar == a` няма да успее да се компилира, защото екземплярите на enum не могат да бъдат приравнени, обаче `if let` ще продължи да работи.

Искате ли предизвикателство? Поправете следния пример като използвате `if let`:

```rust,editable,ignore,mdbook-runnable
// Този 'enum' нарочно не имплементира или наследява PartialEq.
// Това е причината сравнението 'Foo::Bar == a' се проваля по-долу.
enum Foo {Bar}

fn main() {
    let a = Foo::Bar;

    // Променливата 'a' съвпада с Foo::Bar
    if Foo::Bar == a {
    // ^-- това причинява компилационна грешка. Вместо това използвайте `if let`.
        println!("a is foobar");
    }
}
```

### Вижте също

[`Енумерации`][enum], [`Option`][option], и [RFC][if_let_rfc]

[enum]: ../custom_types/enum.md
[if_let_rfc]: https://github.com/rust-lang/rfcs/pull/160
[option]: ../std/option.md
