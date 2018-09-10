# rust-clippy [![translate-svg]][translate-list] 

[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list


「 一系列的lints,以捕捉常见的错误,并改善你的[Rust](https://github.com/rust-lang/rust)代码.  」

[中文](./readme.md) | [english](https://rust-lang-nursery.github.io/rust-clippy/master/index.html)


---

## 校对 🀄️

<!-- doc-templite START generated -->
<!-- repo = 'rust-lang-nursery/rust-clippy' -->
<!-- commit = 'b47b8c223cb8ea61436cd898d8aedc01f2b61b95' -->
<!-- time = '2018 9.7' -->
翻译的原文 | 与日期 | 最新更新 | 更多
---|---|---|---
[commit] | ⏰ 2018 9.7 | ![last] | [中文翻译][translate-list]

[last]: https://img.shields.io/github/last-commit/rust-lang-nursery/rust-clippy.svg
[commit]: https://github.com/rust-lang-nursery/rust-clippy/tree/b47b8c223cb8ea61436cd898d8aedc01f2b61b95

<!-- doc-templite END generated -->

- [ ] [./readme.md](./readme.md)
- [ ] [./index.html](./index.html)
- [ ] [./lints.json](./lints.json)

> 此项目的重心在 `gh-pages`分支, 的 网页内容

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

### 目录

<!-- START doctoc -->
<!-- END doctoc -->


我们目前正在通过RFC流程讨论Clippy 1.0<https://github.com/rust-lang/rfcs/pull/2476>. RFC的目标是阐明有关lint分类的策略以及lint应该在编译器中的策略以及哪些lint应该在Clippy中. 请留意您对RFC PR的看法. 

# 大眼夹

[![Build Status](https://travis-ci.org/rust-lang-nursery/rust-clippy.svg?branch=master)](https://travis-ci.org/rust-lang-nursery/rust-clippy)
[![Windows Build status](https://ci.appveyor.com/api/projects/status/id677xpw1dguo7iw?svg=true)](https://ci.appveyor.com/project/rust-lang-libs/rust-clippy)
[![Current Version](https://meritbadge.herokuapp.com/clippy)](https://crates.io/crates/clippy)
[![License: MPL-2.0](https://img.shields.io/crates/l/clippy.svg)](#license)

一系列的lints,以捕捉常见的错误,并改善你的[锈](https://github.com/rust-lang/rust)码. 

[这个箱子里有275个棉花!](https://rust-lang-nursery.github.io/rust-clippy/master/index.html)

我们有一堆lint类别,允许您选择Clippy应该有多少~~搅扰~~帮你: 

-   `clippy::all` (没有误报的一切) 
-   `clippy::pedantic` (一切) 
-   `clippy::nursery` (尚未准备好的新lints) 
-   `clippy::style` (应该以更惯用的方式编写的代码) 
-   `clippy::complexity` (执行简单但复杂的代码的代码) 
-   `clippy::perf` (可以更快的方式编写的代码) 
-   `clippy::cargo` (检查货物清单) 
-   **`clippy::correctness`** (代码完全错误或非常无用) 

请来更多[提出问题](https://github.com/rust-lang-nursery/rust-clippy/issues)如果你有想法!

目录: 

-   [使用说明](#usage)
-   [组态](#configuration)
-   [执照](#license)

## 用法

由于这是一个帮助库或应用程序开发人员编写更好代码的工具,因此建议不要将Clippy作为硬依赖项包含在内. 选项包括将其用作可选依赖项,货物子命令或构建期间包含的功能. 这些选项详述如下. 

### 作为货物子命令 (`cargo clippy`) 

使用Clippy的一种方法是通过rustup安装Clippy作为货物子命令. 

#### 第1步: 安装rustup

你可以安装[rustup](http://rustup.rs/)在支持的平台上. 这将有助于我们安装clippy及其依赖项. 

如果您已经安装了rustup,请更新以确保您拥有最新的rustup和编译器: 

```terminal
rustup update
```

#### 第2步: 安装夜间工具链

Rustup集成仍然是新的,你需要一个相对较新的夜间 (2018-07-15或更高版本) . 

用Night安装Rust[rustup](https://rustup.rs/): 

```terminal
rustup install nightly
```

#### 第3步: 安装clippy

一旦生锈并安装了夜间工具链,请运行以下命令: 

```terminal
rustup component add clippy-preview --toolchain=nightly
```

现在您可以通过调用来运行Clippy`cargo +nightly clippy`. 如果夜间是你生锈的默认工具链,`cargo clippy`会很好的. 

### 从命令行运行Clippy而不安装它

要使用Clippy编译您的箱子而不在代码中安装Clippy,您可以使用: 

```terminal
cargo run --bin cargo-clippy --manifest-path=path_to_clippys_Cargo.toml
```

*[注意](https://github.com/rust-lang-nursery/rust-clippy/wiki#a-word-of-warning): *确保Clippy编译时使用与此处调用的相同版本的rustc!

## 组态

可以在名为的TOML文件中配置一些lints`clippy.toml`要么`.clippy.toml`. 它包含一个基本的`variable = value`映射例如. 

```toml
blacklisted-names = ["toto", "tata", "titi"]
cyclomatic-complexity-threshold = 30
```

见[lints列表](https://rust-lang-nursery.github.io/rust-clippy/master/index.html)有关可以配置哪些lints以及变量含义的更多信息. 

要取消激活"有关详细信息,请访问*皮棉链接*"你可以定义的消息`CLIPPY_DISABLE_DOCS_LINKS`环境变量. 

### 允许/拒绝lints

您可以添加选项`allow`/`warn`/`deny`: 

-   整套的`Warn`使用的lints`clippy`皮棉组 (`#![deny(clippy::all)]`) 

-   所有的lints都使用了`clippy`和`clippy::pedantic`棉绒组 (`#![deny(clippy::all)]`,`#![deny(clippy::pedantic)]`) . 注意`clippy::pedantic`包含一些非常积极的lint容易出现误报. 

-   只有一些棉绒 (`#![deny(clippy::single_match, clippy::box_vec)]`等) 

-   `allow`/`warn`/`deny`可以限制为单个功能或模块使用`#[allow(...)]`等等

注意: `deny`产生错误而不是警告. 

## 更新rustc

有时候,没有Clippy追赶,rustc会向前移动. 因此,更新rustc可能会使Clippy处于非功能状态,直到我们修复产生的断裂. 

你可以使用[防锈更新](rust-update)仅当Clippy也能正确更新时才更新rustc的脚本. 

## 执照

许可下[MPL](https://www.mozilla.org/MPL/2.0/). 如果您遇到许可证问题,请告诉我,我会尝试将其更改为更宽松的内容. 
