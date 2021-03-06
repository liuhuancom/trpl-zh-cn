## Hello, World!

> [ch01-02-hello-world.md](https://github.com/rust-lang/book/blob/master/second-edition/src/ch01-02-hello-world.md)
> <br>
> commit 4f2dc564851dc04b271a2260c834643dfd86c724

现在你已经安装好了 Rust，让我们来编写你的第一个 Rust 程序。当学习一门新语言的时候，编写一个在屏幕上打印 “Hello, world!” 文本的小程序是一个传统，而在这一部分，我们将遵循这个传统。

> 注意：本书假设你熟悉基本的命令行操作。Rust 本身并不对你的编辑器，工具和你的代码存放在何处有什么特定的要求，所以如果你比起命令行更喜欢 IDE，请随意选择你喜欢的 IDE。

### 创建项目文件夹

首先，创建一个文件夹来编写 Rust 代码。Rust 并不关心你的代码存放在哪里，不过在本书中，我们建议在你的 home 目录创建一个**项目**目录，并把你的所有项目放在这。打开一个终端并输入如下命令来为这个项目创建一个文件夹：

Linux 和 Mac:

```sh
$ mkdir ~/projects
$ cd ~/projects
$ mkdir hello_world
$ cd hello_world
```

Windows:

```cmd
> mkdir %USERPROFILE%\projects
> cd %USERPROFILE%\projects
> mkdir hello_world
> cd hello_world
```

### 编写并运行 Rust 程序

接下来，创建一个新的叫做 *main.rs* 的源文件。Rust 文件总是以 *.rs* 后缀结尾。如果文件名多于一个单词，使用下划线分隔它们。例如，使用 *my_program.rs* 而不是   *myprogram.rs*。

现在打开刚创建的 *main.rs* 文件，并输入如下代码：

<span class="filename">Filename: main.rs</span>

```rust
fn main() {
    println!("Hello, world!");
}
```

保存文件，并回到终端窗口。在 Linux 或 OSX 上，输入如下命令：

```sh
$ rustc main.rs
$ ./main
Hello, world!
```

在 Windows 上，运行`.\main.exe`而不是`./main`。不管使用何种系统，你应该在终端看到`Hello, world!`字符串。如果你做到了，那么恭喜你！你已经正式编写了一个 Rust 程序。你是一名 Rust 程序员了！欢迎入坑。

### 分析 Rust 程序

现在，让我们回过头来仔细看看你的“Hello, world!”程序到底发生了什么。这是谜题的第一片：

```rust
fn main() {

}
```

这几行定义了一个 Rust **函数**。`main` 函数是特殊的：这是每一个可执行的 Rust 程序首先运行的函数（译者注：入口点）。第一行表示“定义一个叫 `main` 的函数，没有参数也没有返回值。”如果有参数的话，它们应该出现在括号中，`(`和`)`。

同时注意函数体被包裹在大括号中，`{`和`}`。Rust 要求所有函数体都位于大括号中（译者注：对比有些语言特定情况可以省略大括号）。将前一个大括号与函数声明置于一行，并留有一个空格被认为是一个好的代码风格。

在`main()`函数中：

```rust
    println!("Hello, world!");
```

这行代码做了这个小程序的所有工作：它在屏幕上打印文本。有很多需要注意的细节。第一个是 Rust 代码风格使用 4 个空格缩进，而不是 1 个制表符（tab）。

第二个重要的部分是`println!()`。这叫做 Rust **宏**，是如何进行 Rust 元编程（metaprogramming）的关键所在。相反如果调用一个函数的话，它应该看起来像这样：`println`（没有`!`）。我们将在 24 章更加详细的讨论 Rust 宏，不过现在你只需记住当看到符号 `!` 的时候，就代表在调用一个宏而不是一个普通的函数。

接下来，`"Hello, world!"` 是一个 **字符串**。我们把这个字符串作为一个参数传递给`println!`，它负责在屏幕上打印这个字符串。轻松加愉快！(⊙o⊙)

这一行以一个分号结尾（`;`）。`;`代表这个表达式的结束和下一个表达式的开始。大部分 Rust 代码行以`;`结尾。

### 编译和运行是两个步骤

在“编写并运行 Rust 程序”部分，展示了如何运行一个新创建的程序。现在我们将拆分并检查每一步操作。

在运行一个 Rust 程序之前，必须编译它。可以输入`rustc`命令来使用 Rust 编译器并像这样传递你源文件的名字：

```sh
$ rustc main.rs
```

如果你来自 C 或 C++ 背景，你会发现这与`gcc`和`clang`类似。编译成功后，Rust 应该会输出一个二进制可执行文件，在 Linux 或 OSX 上在 shell 中你可以通过`ls`命令看到如下：

```sh
$ ls
main  main.rs
```

在 Windows 上，输入：

```cmd
> dir /B %= the /B option says to only show the file names =%
main.exe
main.rs
```

这表示我们有两个文件：*.rs* 后缀的源文件，和可执行文件（在 Windows下是 *main.exe*，其它平台是 *main*）。这里剩下的操作就只有运行 *main* 或 *main.exe* 文件了，像这样：

```sh
$ ./main  # or .\main.exe on Windows
```

如果 *main.rs* 是我们的“Hello, world!”程序，它将会在终端上打印`Hello, world!`。

来自 Ruby、Python 或 JavaScript 这样的动态类型语言背景的同学，可能不太习惯在分开的步骤编译和执行程序。Rust 是一种 **静态提前编译语言**（*ahead-of-time compiled language*），这意味着可以编译好程序后，把它给任何人，他们都不需要安装 Rust 就可运行。如果你给他们一个 `.rb` ， `.py` 或 `.js` 文件，他们需要先分别安装 Ruby，Python，JavaScript 实现（运行时环境，VM），不过你只需要一句命令就可以编译和执行程序。这一切都是语言设计的权衡取舍。

仅仅使用`rustc`编译简单程序是没问题的，不过随着项目的增长，你将想要能够控制你项目拥有的所有选项，并使其易于分享你的代码给别人或别的项目。接下来，我们将介绍一个叫做 Cargo 的工具，它将帮助你编写现实生活中的 Rust 程序。

## Hello, Cargo!

Cargo 是 Rust 的构建系统和包管理工具，同时 Rustacean 们使用 Cargo 来管理它们的 Rust 项目，因为它使得很多任务变得更轻松。例如，Cargo负责构建代码、下载代码依赖的库并编译这些库。我们把代码需要的库叫做 **依赖**（*dependencies*）。

最简单的 Rust 程序，例如我们刚刚编写的，并没有任何依赖，所以目前我们只使用了 Cargo 负责构建代码的部分。随着你编写更加复杂的 Rust 程序，你会想要添加依赖，那么如果你使用 Cargo 开始的话，这将会变得简单许多。

由于绝大部分 Rust 项目使用 Cargo，本书接下来的部分将假设你使用它。如果使用安装章节介绍的官方安装包的话，Rust 自带 Cargo。如果通过其他方式安装 Rust 的话，可以在终端输入如下命令检查是否安装了 Cargo：

```sh
$ cargo --version
```

如果看到了版本号，一切 OK！如果出现一个类似“`command not found`”的错误，那么你应该查看安装方式的文档来确定如何单独安装 Cargo。

### 使用 Cargo 创建项目

让我们使用 Cargo 来创建一个新项目并看看与`hello_world`项目有什么不同。回到项目目录（或者任何你决定放置代码的目录）：

Linux 和 Mac:

```sh
$ cd ~/projects
```

Windows:

```cmd
> cd %USERPROFILE%\projects
```

并在任何操作系统运行：

```sh
$ cargo new hello_cargo --bin
$ cd hello_cargo
```

我们向`cargo new`传递了`--bin`因为我们的目标是生成一个可执行程序，而不是一个库。可执行文件是二进制可执行文件，通常就叫做 **二进制文件**（*binaries*）。项目的名称被定为`hello_cargo`，同时 Cargo 在一个同名（子）目录中创建它的文件，接着我们可以进入查看。

如果列出 *hello_cargo* 目录中的文件，我们将会看到 Cargo 生成了两个文件和一个目录：一个 *Cargo.toml* 文件和一个 *src* 目录，*main.rs* 文件位于目录中。它也在 *hello_cargo* 目录初始化了一个 git 仓库，以及一个 *.gitignore* 文件；你可以改为使用不同的版本控制系统，或者不使用，通过`--vcs`参数。

使用你选择的文本编辑器（IDE）打开 *Cargo.toml* 文件。它应该看起来像这样：

<span class="filename">Filename: Cargo.toml</span>

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]

[dependencies]
```

这个文件使用[*TOML*][toml]<!-- ignore --> (Tom's Obvious, Minimal Language) 格式。TOML 类似于 INI，不过有一些额外的改进之处，并且被用作 Cargo 的配置文件的格式。

[toml]: https://github.com/toml-lang/toml

第一行，`[package]`，是一个部分标题表明下面的语句用来配置一个包。随着我们在这个文件增加更多的信息，我们还会增加其他部分。

最后一行，`[dependencies]`，是列出项目依赖的 *crates*（我们这么称呼 Rust 代码的包）的部分的开始，这样 Cargo 也就知道去下载和编译它们。这个项目并不需要任何其他的 crate，不过在猜猜看教程章节会需要。

现在看看 *src/main.rs*：

```rust
fn main() {
    println!("Hello, world!");
}
```

Cargo 为你生成了一个“Hello World!”，正如我们之前编写的那个！目前为止我们所见过的之前项目与 Cargo 生成的项目区别有：

- 代码位于 *src* 目录
- 项目根目录包含一个 *Cargo.toml* 配置文件

Cargo 期望源文件位于 src 目录，这样将项目根目录留给 README、license 信息、配置文件和其他跟代码无关的文件。这样，Cargo 帮助你保持项目干净整洁。一切井井有条。

如果没有使用 Cargo 开始项目，正如我们在 *hello_world* 目录中的项目，可以把它转化为一个 Cargo 使用的项目，通过将代码放入 *src* 目录并创建一个合适的 *Cargo.toml*。

### 构建并运行 Cargo 项目

现在让我们看看通过 Cargo 构建和运行 Hello World 程序有什么不同。为此，我们输入如下命令：

```
$ cargo build
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
```

这应该创建 *target/debug/hello_cargo*（或者在 Windows 上是 *target\debug\hello_cargo.exe*）可执行文件，可以通过这个命令运行：

```sh
$ ./target/debug/hello_cargo # or .\target\debug\hello_cargo.exe on Windows
Hello, world!
```

好的！如果一切顺利，`Hello, world!`应该再次打印在终端上。

第一次运行的时候也会使 Cargo 在项目根目录创建一个叫做 *Cargo.lock* 的新文件，它看起来像这样：

<span class="filename">Filename: Cargo.lock</span>

```toml
[root]
name = "hello_cargo"
version = "0.1.0"
```

Cargo 使用 *Cargo.lock* 来记录程序的依赖。这个项目并没有依赖，所以内容有一点稀少。事实上，你自己永远也不需要碰这个文件；仅仅让 Cargo 处理它就行了。

我们刚刚使用`cargo build`构建了项目并使用`./target/debug/hello_cargo`运行了它，不过也可以使用`cargo run`编译并运行：

```sh
$ cargo run
     Running `target/debug/hello_cargo`
Hello, world!
```

注意这一次，并没有出现告诉我们 Cargo 正在编译 `hello_cargo` 的输出。Cargo 发现文件并没有被改变，所以只是运行了二进制文件。如果修改了源文件的话，将会出现像这样的输出：

```sh
$ cargo run
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
     Running `target/debug/hello_cargo`
Hello, world!
```

所以又出现一些更多的不同：

- 使用`cargo build`构建项目（或使用`cargo run`一步构建并运行），而不是使用`rustc`
- 不同于将构建结果放在源码相同目录，Cargo 会将它放到 *target/debug* 目录中的文件，我们将会看到

Cargo 的另一个有点是不管你使用什么操作系统它的命令都是一样的，所以之后我们将不再为 Linux 和 Mac 以及 Windows 提供特定的命令。

### 发布构建

当项目最终准备好发布了，可以使用`cargo build --release`来优化编译项目。这会在 *target/release* 下生成可执行文件，而不是 *target/debug*。这些优化可以让 Rust 代码运行的更快，不过启用他们会让程序花更长的时间编译。这也是为何这是两种不同的配置：一个为了开发，这时你经常想要快速重新构建；另一个构建提供给用户的最终程序，这时并不会重新构建并希望能运行得越快越好。如果你在测试代码的运行时间，请确保运行`cargo build --release`并使用 *target/release* 下的可执行文件进行测试。

### 把 Cargo 当作习惯

对于简单项目， Cargo 并不能比`rustc`提供更多的价值，不过随着开发的进行终将体现它的价值。对于拥有多个 crate 的复杂项目，可以仅仅运行`cargo build`，然后一切将有序运行。即便这个项目很简单，现在它使用了很多接下来你 Rust 程序生涯将会用到的实用工具。事实上，无形中你可以使用下面的命令开始所有你想要从事的项目：

```sh
$ git clone someurl.com/someproject
$ cd someproject
$ carg
```

> 注意：如果你想要查看 Cargo 的更多细节，请阅读官方的 [Cargo guide]，它覆盖了其所有的功能。

[Cargo guide]: http://doc.crates.io/guide.html