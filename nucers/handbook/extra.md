# 拓展语法

> 这里的语法, 不同的编辑器支持程度不相同

## 高亮行内文本

```markdown
这有一段==高亮==文本
```

输出

这有一段==高亮==文本

## Checkbox

```markdown
- [ ] 项目一未选择
- [x] 项目二已选择
```

输出

- [ ] 项目一未选择
- [x] 项目二已选择

## GitHub Diff

> GitHub Diff是用于直观反映文档修改情况的一种语法, vditor并未完全实现GitHub的Diff语法

````markdown
```diff
+ 新增内容
- 删除内容
```
````

输出

```diff
+ 新增内容
- 删除内容
```

## 绘文字(emoji)

> 支持emoji短码插入

```markdown
中国 :cn:
```

输出

中国 :cn:

## Tex

> Tex是广泛用于数学、物理和各类论文格式控制的一种语法, 但是在此仅用于公式的输入, 不能用于格式的控制, 该部分的实现基于 [KaTex](https://katex.org/)

### 行内数学公式

```markdown
质能方程 $E = mc^2$
```

输出

质能方程 $E = mc^2$

### 数学公式块

麦克斯韦方程组

```markdown
$$
\nabla \times H = J + \frac{\partial D}{\partial t} \newline
\nabla \times E = - \frac{\partial B}{\partial t} \newline
\nabla \cdot B = 0 \newline
\nabla \cdot D = \rho
$$
```

输出

$$
\nabla \times H = J + \frac{\partial D}{\partial t} \newline
\nabla \times E = - \frac{\partial B}{\partial t} \newline
\nabla \cdot B = 0 \newline
\nabla \cdot D = \rho
$$

## 媒体插入

> 自动识别媒体链接并且渲染

视频demo

http://chimee.org/vod/1.mp4

音频demo

http://stor.cloudmusics.cn/mp3/2020/01/727f6d5495b821b2c87d70c29a83a4d9.mp3http://stor.cloudmusics.cn/mp3/2020/01/727f6d5495b821b2c87d70c29a83a4d9.mp3

> 恭喜您已完成拓展语法部分, 之后将进入图表部分等实现更高阶的玩法
