# Замразяване

Когато данните се свържат с едно и също име като **не мутиращи**, те стават *замразени (freeze)*.
*Замразените* данни не могат да бъдат променяни, докато **не мутиращата** променлива излезе от обхват:

```rust,editable,ignore,mdbook-runnable
fn main() {
    let mut _mutable_integer = 7i32;

    {
        // Презаписване чрез не мутиращата `_mutable_integer`
        let _mutable_integer = _mutable_integer;

        // Грешка! `_mutable_integer` е замразена в този обхват
        _mutable_integer = 50;
        // FIXME ^ Коментирайте този ред

        // `_mutable_integer` излиза от обхват
    }

    // ОК! `_mutable_integer` не е замразена в този обхват
    _mutable_integer = 3;
}
```
