# 枚举和模式匹配

> [ch06-00-enums.md](https://github.com/rust-lang/book/blob/master/src/ch06-00-enums.md)
> <br>
> commit 396e2db4f7de2e5e7869b1f8bc905c45c631ad7d

本章介绍**枚举**，也被称作 *enums*。枚举允许你通过列举可能的值来定义一个类型。首先，我们会定义并使用一个枚举来展示它是如何连同数据一起编码信息的。接下来，我们会探索一个特别有用的枚举，叫做`Option`，它代表一个值要么是一些值要么什么都不是。然后会讲到`match`表达式中的模式匹配如何使对枚举不同的值运行不同的代码变得容易。最后会涉及到`if let`，另一个简洁方便处理代码中枚举的结构。

枚举是一个很多语言都有的功能，不过不同语言中的功能各不相同。Rust 的枚举与像F#、OCaml 和 Haskell这样的函数式编程语言中的**代数数据类型**（*algebraic data types*）最为相似。