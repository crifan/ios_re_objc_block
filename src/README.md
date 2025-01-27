# iOS逆向开发：Block匿名函数

* 最新版本：`v0.7.1`
* 更新时间：`20241026`

## 简介

介绍iOS逆向期间会涉及到的Block匿名回调函数。先解释为何要研究Block；再详细介绍Block，包括正向开发时的如何写Block代码，然后是逆向时Block的结构定义，包括定义的代码和定义的结构图，再分别介绍每一部分的含义，包括Block类型、flags、invoke，以及其中的signature函数签名，以及descriptor、imported variables引用的量；再介绍iOS逆向期间所涉及到的Block最核心的内容是哪些，然后举例详细阐述如何通过Block搞懂函数调用逻辑，以及导入变量的参数传递，顺带介绍如何优化IDA伪代码。然后再整理Block相关的心得，比如动态调试期间，如何查看Block信息、和Block相关的objc函数。

## 源码+浏览+下载

本书的各种源码、在线浏览地址、多种格式文件下载如下：

### HonKit源码

* [crifan/ios_re_objc_block: iOS逆向开发：Block匿名函数](https://github.com/crifan/ios_re_objc_block)

#### 如何使用此HonKit源码去生成发布为电子书

详见：[crifan/honkit_template: demo how to use crifan honkit template and demo](https://github.com/crifan/honkit_template)

### 在线浏览

* [iOS逆向开发：Block匿名函数 book.crifan.org](https://book.crifan.org/books/ios_re_objc_block/website/)
* [iOS逆向开发：Block匿名函数 crifan.github.io](https://crifan.github.io/ios_re_objc_block/website/)

### 离线下载阅读

* [iOS逆向开发：Block匿名函数 PDF](https://book.crifan.org/books/ios_re_objc_block/pdf/ios_re_objc_block.pdf)
* [iOS逆向开发：Block匿名函数 ePub](https://book.crifan.org/books/ios_re_objc_block/epub/ios_re_objc_block.epub)
* [iOS逆向开发：Block匿名函数 Mobi](https://book.crifan.org/books/ios_re_objc_block/mobi/ios_re_objc_block.mobi)

## 版权和用途说明

此电子书教程的全部内容，如无特别说明，均为本人原创。其中部分内容参考自网络，均已备注了出处。如发现有侵权，请通过邮箱联系我 `admin 艾特 crifan.com`，我会尽快删除。谢谢合作。

各种技术类教程，仅作为学习和研究使用。请勿用于任何非法用途。如有非法用途，均与本人无关。

## 鸣谢

感谢我的老婆**陈雪**的包容理解和悉心照料，才使得我`crifan`有更多精力去专注技术专研和整理归纳出这些电子书和技术教程，特此鸣谢。

## 其他

### 作者的其他电子书

本人`crifan`还写了其他`150+`本电子书教程，感兴趣可移步至：

[crifan/crifan_ebook_readme: Crifan的电子书的使用说明](https://github.com/crifan/crifan_ebook_readme)

### 关于作者

关于作者更多介绍，详见：

[关于CrifanLi李茂 – 在路上](https://www.crifan.org/about/)
