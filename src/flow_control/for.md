# for цикли

## for и range

Конструкцията `for in` може да се използва, за да се итерира даден `Iterator`.
Един от най-лесните начини за създаване на итератор е да използвате нотацията **range** `a..b`.
Това дава стойности от `a` (включително) до `b`
на стъпки от една.

Нека напишем FizzBuzz използвайки `for` вместо `while`.

```rust,editable
fn main() {
    // `n` ще бъде стойностите: 1, 2, ..., 100 във всяка итерация
    for n in 1..101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

Като алтернатива, `a..=b` може да се използва за диапазон, който включва и двата краища.
Горното може да се запише като:

```rust,editable
fn main() {
    // `n` ще бъде стойностите: 1, 2, ..., 100 във всяка итерация
    for n in 1..=100 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

## for и iterators

Конструкцията `for in` е в състояние да взаимодейства с  `Iterator` по няколко начина.
Както беше обсъдено в раздела за [Iterator][iter], по подразбиране `for`
цикъла ще приложи функцията `into_iter` към колекцията. Това обаче
не е единственото средство за преобразуване на колекции в итератори.

`into_iter`, `iter` и `iter_mut` всички обработват конвертирането на колекция
в итератор по различни начини, като предоставят различни изгледи на данните в нея.

* `iter` - Този реферира всеки елемент от колекцията през всяка итерация.
  По този начин колекцията остава недокосната и достъпна за повторна употреба след цикъла.

```rust,editable
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.iter() {
        match name {
            &"Ferris" => println!("There is a rustacean among us!"),
            // TODO ^ Опитайте да изтриете '&' и да съпоставите само "Ferris"
            _ => println!("Hello {}", name),
        }
    }
    
    println!("names: {:?}", names);
}
```

* `into_iter` - Този консумира колекцията така че при всяка итерация се дава точни данни.
  След като колекцията бъде изконсумирана, вече не е
  наличен за повторна употреба, тъй като е бил `преместен` в рамките на цикъла.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.into_iter() {
        match name {
            "Ferris" => println!("There is a rustacean among us!"),
            _ => println!("Hello {}", name),
        }
    }
    
    println!("names: {:?}", names);
    // FIXME ^ Коментирайте този ред
}
```

* `iter_mut` - Този реферира всеки елемент от колекцията през всяка итерация, но позволява тя да бъде модифицирана на място.

```rust,editable
fn main() {
    let mut names = vec!["Bob", "Frank", "Ferris"];

    for name in names.iter_mut() {
        *name = match name {
            &mut "Ferris" => "There is a rustacean among us!",
            _ => "Hello",
        }
    }

    println!("names: {:?}", names);
}
```

В горните откъси забележете типа на отклонението `match`, това е ключовата разлика в типовете на итерация.
Разликата в типа след това, разбира се,
подразбира различни действия, които могат да бъдат извършени.

### Вижте също

[Итератори][iter]

[iter]: ../trait/iter.md
