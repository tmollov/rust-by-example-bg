# Изрази

Една програма на **Rust** се състои (предимно) от поредица от инструкции:

```rust,editable
fn main() {
    // инструкция 1
    // инструкция 2
    // инструкция 3
}
```

В Rust има няколко вида инструкции. Най-често срещаните две са
деклариране на променливи и използване на израза `;`:

```rust,editable
fn main() {
    // деклариране на променливи
    let x = 5;

    // израз;
    x;
    x + 1;
    15;
}
```

Блоковете също са изрази и могат да бъдат използвани като стойности в присвоявания.
Последният израз в блока ще бъде присвоен на мястото на израза, като например локална променлива.
Въпреки това, ако последният израз в блока завършва с точка и запетая, стойността, която се връща, ще бъде `()`.

```rust,editable
fn main() {
    let x = 5u32;

    let y = {
        let x_squared = x * x;
        let x_cube = x_squared * x;

        // Този израз ще бъде присвоен на `y`
        x_cube + x_squared + x
    };

    let z = {
        // Точката и запетая потискат този израз и `()` се присвоява на `z`
        2 * x;
    };

    println!("x is {:?}", x);
    println!("y is {:?}", y);
    println!("z is {:?}", z);
}
```
