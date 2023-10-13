# use

Декларирането на `use` може да се използва, за да не се изисква ръчно определяне на обхвата:

```rust,editable
// Атрибут, който скрива предупрежденията за неползван код.
#![allow(dead_code)]

enum Status {
    Rich,
    Poor,
}

enum Work {
    Civilian,
    Soldier,
}

fn main() {
    // Дефинираме `use` за всяко име, така че те да бъдат налични без ръчно определен обхват.
    use crate::Status::{Poor, Rich};
    // Автоматично използваме всичко от обхвата на `Work` чрез `use`.
    use crate::Work::*;

    // Еквивалентно на `Status::Poor`.
    let status = Poor;
    // Еквивалентно на `Work::Civilian`.
    let work = Civilian;

    match status {
        // Забележете липсата на обхват поради изричния `use` по-горе.
        Rich => println!("The rich have lots of money!"),
        Poor => println!("The poor have no money..."),
    }

    match work {
        // Забележете отново липсата на обхват поради.
        Civilian => println!("Civilians work!"),
        Soldier  => println!("Soldiers fight!"),
    }
}
```

### Вижте също

[`match`][match] и [`use`][use]

[use]: ../../mod/use.md
[match]: ../../flow_control/match.md
