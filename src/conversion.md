# Конвертиране

Примитивните типове могат да се конвертират един в друг чрез [кастване].

Rust адресира конвертиранията между персонализирани типове (като `struct` и `enum`) като използва [traits].
Генеричните преобразувания ще използват `trait`-овете [`From`] и [`Into`].
Има обаче по-специфични за по-често срещаните случаи,
по-специално при преобразуване в или от типа `String`.

[кастване]: types/cast.md
[traits]: trait.md
[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html
