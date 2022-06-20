# Go 1.19要来了，看看都有哪些变化

## 前言

Go官方团队在2022.06.11发布了Go 1.19 Beta 1版本，Go 1.19的正式release版本预计会在今年8月份发布。

让我们先睹为快，看看Go 1.19给我们带来了哪些变化。

这是Go 1.19版本更新内容详解的第2篇，欢迎大家关注公众号，及时获取本系列最新更新。

## Go 1.19发布清单

和Go 1.18相比，改动相对较小，主要涉及语言(Language)、内存模型(Memory Model)、可移植性(Ports)、Go Tool工具链、运行时(Runtime)、编译器(Compiler)、汇编器(Assembler)、链接器(Linker)和核心库(Core library)等方面的优化。

第1篇详细介绍了Go 1.19在语言、内存模型、可移植性方面的改进，本文重点介绍Go 1.19版本在Go Tool工具链方面的变化。

### Doc Comments

Go 1.19 adds support for links, lists, and clearer headings in doc comments. As part of this change, [`gofmt`](https://tip.golang.org/cmd/gofmt) now reformats doc comments to make their rendered meaning clearer. See “[Go Doc Comments](https://tip.golang.org/doc/comment)” for syntax details and descriptions of common mistakes now highlighted by `gofmt`. As another part of this change, the new package [go/doc/comment](https://tip.golang.org/pkg/go/doc/comment) provides parsing and reformatting of doc comments as well as support for rendering them to HTML, Markdown, and text.

### New `unix` build constraint

The build constraint `unix` is now recognized in `//go:build` lines. The constraint is satisfied if the target operating system, also known as `GOOS`, is a Unix or Unix-like system. For the 1.19 release it is satisfied if `GOOS` is one of `aix`, `android`, `darwin`, `dragonfly`, `freebsd`, `hurd`, `illumos`, `ios`, `linux`, `netbsd`, `openbsd`, or `solaris`. In future releases the `unix` constraint may match additional newly supported operating systems.

### Go command

The `-trimpath` flag, if set, is now included in the build settings stamped into Go binaries by `go` `build`, and can be examined using [`go` `version` `-m`](https://pkg.go.dev/cmd/go#hdr-Print_Go_version) or [`debug.ReadBuildInfo`](https://pkg.go.dev/runtime/debug#ReadBuildInfo).

`go` `generate` now sets the `GOROOT` environment variable explicitly in the generator's environment, so that generators can locate the correct `GOROOT` even if built with `-trimpath`.

`go` `test` and `go` `generate` now place `GOROOT/bin` at the beginning of the `PATH` used for the subprocess, so tests and generators that execute the `go` command will resolve it to same `GOROOT`.

`go` `env` now quotes entries that contain spaces in the `CGO_CFLAGS`, `CGO_CPPFLAGS`, `CGO_CXXFLAGS`, `CGO_FFLAGS`, `CGO_LDFLAGS`, and `GOGCCFLAGS` variables it reports.

The `go` command now caches information necessary to load some modules, which should result in a speed-up of some `go` `list` invocations.

### Vet

The `vet` checker “errorsas” now reports when [`errors.As`](https://tip.golang.org/pkg/errors/#As) is called with a second argument of type `*error`, a common mistake.

**想了解Go泛型的使用方法、设计思路和最佳实践，推荐大家阅读**：

* [官方教程：Go泛型入门](https://mp.weixin.qq.com/s?__biz=Mzg2MTcwNjc1Mg==&mid=2247483720&idx=1&sn=57ec4877dfd364a59deacf1e74a4fb66&chksm=ce124e27f965c731432dcc89d1e0563cf84baaef482eaa068a91bee61f10cf85b433923b83b4&token=1782465473&lang=zh_CN#rd)
* [一文读懂Go泛型设计和使用场景](https://mp.weixin.qq.com/s?__biz=Mzg2MTcwNjc1Mg==&mid=2247483731&idx=1&sn=b2258b28e2f3c16b065a5a1b22c15b0d&chksm=ce124e3cf965c72a6a22e0ed15deda8238567407bbd7157a79753fc8b605727ab2153009493c&token=1782465473&lang=zh_CN#rd)
* [重磅：Go 1.18将移除用于泛型的constraints包](https://mp.weixin.qq.com/s?__biz=Mzg2MTcwNjc1Mg==&mid=2247483855&idx=1&sn=6ab4aeb140a1a08268dc8a0284a6f375&chksm=ce124ea0f965c7b6776061960d71e4ffb30484a82041f5b1d4786c4b49c4ffabc07a28b1cd48&token=1782465473&lang=zh_CN#rd)
* [泛型最佳实践：Go泛型设计者教你如何用泛型](https://mp.weixin.qq.com/s?__biz=Mzg2MTcwNjc1Mg==&mid=2247484015&idx=1&sn=576b2d8b84b3a8ce5bdd6952c2b84062&chksm=ce124d00f965c416b07dcb81c4dcb9cf75859b2787d4f00ec8c80b37ca42e58cc651420a3b33&token=1782465473&lang=zh_CN#rd)



**想了解Go原子操作和使用方法，推荐大家阅读**：

* [Go并发编程之原子操作sync/atomic](https://mp.weixin.qq.com/s?__biz=Mzg2MTcwNjc1Mg==&mid=2247484082&idx=1&sn=934787c9829391ba743bd611818ad0e2&chksm=ce124dddf965c4cb7d0f2d9d001ab4b7d949fbe87c4c8b7ee8d7498946824ec9aa6581cfe986&token=1782465473&lang=zh_CN#rd)



## 总结

下一篇会介绍Go 1.19在运行时、编译器、汇编器、链接器和核心库的优化工作，有一些内容值得学习，欢迎大家保持关注。



## 开源地址

文章和示例代码开源在GitHub: [Go语言初级、中级和高级教程](https://github.com/jincheng9/go-tutorial)。

公众号：coding进阶。关注公众号可以获取最新Go面试题和技术栈。

个人网站：[Jincheng's Blog](https://jincheng9.github.io/)。

知乎：[无忌](https://www.zhihu.com/people/thucuhkwuji)。



## 福利

我为大家整理了一份后端开发学习资料礼包，包含编程语言入门到进阶知识(Go、C++、Python)、后端开发技术栈、面试题等。

关注公众号「coding进阶」，发送消息 **backend** 领取资料礼包，这份资料会不定期更新，加入我觉得有价值的资料。还可以发送消息「**进群**」，和同行一起交流学习，答疑解惑。



## References

* https://tip.golang.org/doc/go1.19
* https://tip.golang.org/doc/comment