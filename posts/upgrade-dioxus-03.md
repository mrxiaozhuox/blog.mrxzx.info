---
title: Upgrade your project to Dioxus v0.3.X
tags: [dioxus]
category: Develop
date: 2023-03-07
released: true
---

In this month, **Dioxus** published `v0.3.2` version, there have many incompatible change for API, so if you have a old Dioxus project and you want to upgrade your Dioxus version, you need do some API change.



## Core & Package Change

### Package Split

In Dioxus `v0.2.X` we use `features` to split & switch package, for example, the different with **Web** and **Desktop** project:

```toml
dioxus = { version = "0.2.4", features = ["web", "router"] }
```

```toml
dioxus = { version = "0.2.5", features = ["desktop", "fermi"] }
```

We just need import a `dioxus` package, and open different features.



But for the `v0.3.2` , Dioxus split all packages, and published many different crates on [crates.io](https://crates.io/search?q=dioxus), so we need import different creates to our project:

```toml
dioxus = { version = "0.3.1" }
dioxus-web = "0.3.1"
dioxus-router = "0.3.0"
fermi = "0.3.0"
```

> But all packages still save in the Dioxus main repo (monorepo) 



### Base Hook Function

sometime we need use `cx.use_hook` to create & maintain a hook, in the `v0.3.X` this function removed closure argument:

```rust
fn component_1(cx: Scope) -> Element {
  cx.use_hook(|| {
    // do some thing ...
  });
  cx.render(rsx! { h1 { "Hello World" } })
}
```



### Lowercase Components

Currently, `Dioxus` supported lowercase components name:

```rust
header {}              ❌
module::header {}      ❌
my_header {}           ✅
```

