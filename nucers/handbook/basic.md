# Nucers编辑器基础

> 此部分适用于完全对于Markdown没有了解的小白入门

## 写在前面的

Nucers的编辑器基于 [vditor](https://github.com/Vanessa219/vditor) 进行了定制化的开发, 兼容所有的 [CommonMark](https://commonmark.org/) 规范, 并在此基础上实现了非标准的语法。Markdown是一种轻量型标记语言, 广泛被程序员所使用, 常用于文档的书写。由于Markdown的基础语法十分的简洁, 并不能满足定制化、个性化的需求, 因此不同的厂商或者编辑器或多或少都在此基础上定制了一些奇奇怪怪的语法, 其中某些语法即使没有成为通用规范也被广大的编辑器所支持。

GitHub上有大量与Markdown编译渲染相关的开源项目 (eg. marked.js, markdown-it), 实现的思路主要有两类: 一、正则匹配；二、编译原理。其中绝大多数都采用了正则表达式匹配的方式实现，但也带来了一定的性能问题。在此之前基于for-editor, [我 @惒泊](https://github.com/HerbertHe)也曾实现过 [for-editor-herb](https://github.com/HerbertHe/for-editor-herb) 的项目, 被某些项目使用过。在那个项目中, 处理了数个issues并且实现了数个features, 通读参考了marked.js的源码实现, 但在大量文本渲染的情况处理的时候会涉及到性能的一些问题, 从而降低用户体验。编辑器的从零实现是一个很困难的事情, 在知乎上就有过探讨富文本编辑器实现的问题, 最主要的是不同浏览器的差异问题及Selection的处理问题。

在Nucers编辑器的选型上, 我们花费了大量的时间去查看第三方的开源项目。作为Nucers的产品经理, 对于Nucers的发展目标是打造一个跨学科、跨平台的面向未来的社区, 给目标用户最佳的体验。

**vditor**基于MIT协议开源, 之前由 [@mxwbq](https://github.com/mxwbq) 同学基于b3log的开源项目实现了 「 中北大学大数据协会论坛 - 听雨轩 (已挂) 」的编辑器即是vditor的发展历史。为了高度定制化的开发和代码风险可控, 我们也同时积极参与了**vditor**及其解析引擎 [lute](https://github.com/88250/lute) 的社区贡献, 同时也欢迎大家使用 [思源笔记](https://github.com/siyuan-note/siyuan) (如果需要的话)

> 需要注意的是, Nucers的编辑器是基于**vditor**实现, 但并不与vditor的表现完全一致 (其中考虑了很多应用场景和安全性问题), 请使用Nucers编辑器文档支持的兼容语法以达到最佳的体验

## 基础标准语法

> Markdown由不同的符号控制着不同的格式, 不同的格式之间请空行, 以达到最佳的用户体验

### 标题

标题共分为六级, 最大的为一级标题, 不同等级标题为父子嵌套关系 (不建议标题等级超过四级, 请妥善规划文章结构)

```markdown
# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题
```

### 段落

> 不同的段落之间请空行, 在段落内部可以使用行内语法来进行不同文字样式的渲染

- 段落换行

```markdown
这是第一段文本

这是第二段文本
```

- 斜体

```markdown
这是一段*斜体*文字
```

输出

这是一段*斜体*文字

- 加粗

```markdown
这是一段**加粗**文字
```

输出

这是一段**加粗**文字

- 加粗斜体

```markdown
这是一段***加粗斜体***文字
```

输出

这是一段***加粗斜体***文字

- 删除线

```markdown
这是一段~~删除文字~~
```

输出

这是一段~~删除文字~~

- 下划线

> 注意, Markdown默认不支持下划线, 这是使用HTML实现的

```markdown
文字中有<u>下划线</u>
```

输出

文字中有<u>下划线</u>

- Keyboard

> Markdown默认不支持Keyboard, 使用HTML实现

```markdown
文字中有<kbd>Keyboard</kbd>
```

输出

文字中有<kbd>Keyboard</kbd>

### 链接

> 使用 `[文字](链接地址)` 的可以插入链接 (支持绝对路径、相对路径和锚点)

```markdown
链接去[百度](https://www.baidu.com)
```

输出

链接去[百度](https://www.baidu.com)

### 图片

> 使用 `![文字](图片地址)` 可以插入图片

```markdown
![知乎头像](https://pic1.zhimg.com/v2-e515915f89e2f4540bf8c9a2046f5107_is.jpg)
```

输出

![知乎头像](https://pic1.zhimg.com/v2-e515915f89e2f4540bf8c9a2046f5107_is.jpg)

### 引用块

引用块常用于对别人的内容进行引用

```markdown
> “世界以痛吻我，我要报之以歌” ——《飞鸟集》
```

输出

> “世界以痛吻我，我要报之以歌” ——《飞鸟集》

### 列表

> 列表的层级是可以嵌套的, 以缩进区分层级

#### 无序列表

```markdown
- 项目一
    - 子项目
    - 子项目2
- 项目二
- 项目三
```

输出

- 项目一
  - 子项目
  - 子项目2
- 项目二
- 项目三

#### 有序列表

```markdown
1. 项目1
2. 项目2
3. 项目3
```

输出

1. 项目1
2. 项目2
3. 项目3

### 代码

- 行内代码

```markdown
本行内我嵌入了一条JavaScript行内代码 `console.log("Hello World")`
```

- 代码块

基本格式

````markdown
```语言类型
代码内容
```
````

举个例子

````markdown
```go
package main

import (
    "fmt"
)

func main() {
    fmt.Println("Hello World")
}
```
````

输出

```go
package main

import (
    "fmt"
)

func main() {
    fmt.Println("Hello World")
}
```

### 表格

语法格式

```markdown
| 表头 | 表头 |
| 对齐控制 | 对齐控制 |
| 表格内容 | 表格内容 |
| 表格内容 | 表格内容 |
```

举个例子

```markdown
| 默认对齐 | 左对齐 | 右对齐 | 居中对齐 |
| -------- | :----- | -----: | :------: |
| 默认     | 👈      |      👉 |   居中   |
```

输出

| 默认对齐 | 左对齐 | 右对齐 | 居中对齐 |
| -------- | :----- | -----: | :------: |
| 默认     | 👈      |      👉 |   居中   |

### 折叠块

> Markdown默认没有此语法, 基于HTML实现

```markdown
<details>
<summary>标题</summary>

被折叠的内容

</details>
```

输出

<details>
<summary>标题</summary>

被折叠的内容

</details>

> 至此, 通用的Markdown语法已经完成!
