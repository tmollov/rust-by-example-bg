# let-else

> 🛈 стабилна от версия: rust 1.65
>
> 🛈 можете да се използвате конкретна версия, като използвате компилатора **rustc** така:
> `rustc --edition=2021 main.rs`

С тази опровергаема стуктура, `let`-`else` може да противопоставя и обвързва променливи
в околния обхват като нормален `let`, или **else** разклонение (напр. `break`,
`return`, `panic!`) когато стойността не съвпада.

```rust
use std::str::FromStr;

fn get_count_item(s: &str) -> (u64, &str) {
    let mut it = s.split(' ');
    let (Some(count_str), Some(item)) = (it.next(), it.next()) else {
        panic!("Can't segment count item pair: '{s}'");
    };
    let Ok(count) = u64::from_str(count_str) else {
        panic!("Can't parse integer: '{count_str}'");
    };
    (count, item)
}

fn main() {
    assert_eq!(get_count_item("3 chairs"), (3, "chairs"));
}
```

Обхватът на обвързаните имена е основното нещо, което прави това различно от
`match` и `if let`-`else` изразите. Приблизително можете да съпоставите
тези модели с жалко повторение и външен `let` блок:

```rust
# use std::str::FromStr;
# 
# fn get_count_item(s: &str) -> (u64, &str) {
#     let mut it = s.split(' ');
    let (count_str, item) = match (it.next(), it.next()) {
        (Some(count_str), Some(item)) => (count_str, item),
        _ => panic!("Can't segment count item pair: '{s}'"),
    };
    let count = if let Ok(count) = u64::from_str(count_str) {
        count
    } else {
        panic!("Can't parse integer: '{count_str}'");
    };
#     (count, item)
# }
# 
# assert_eq!(get_count_item("3 chairs"), (3, "chairs"));
```

### Вижте също

[option][option], [match][match], [if let][if_let] и [let-else RFC][let_else_rfc].

[match]: ./match.md
[if_let]: ./if_let.md
[let_else_rfc]: https://rust-lang.github.io/rfcs/3137-let-else.html
[option]: ../std/option.md
