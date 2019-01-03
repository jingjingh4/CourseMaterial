**目录**

[TOC]

markdown 是一个轻量级标记语言[^1]，它的名称是为了对应 HTML 中的 Markup 对应的语言，提供了简介快速的语法来实现 Markup 的功能。因此 markdown 兼容了 HTML 的标签，此外还可以直接用任何常规的文本编辑器编辑。而本文档的内容主要是描述一些常用 markdown 语法，包括两个方面的内容：1）基本格式语法；2）常用的数学表达式。

**Note**：所有的文件是使用的 [Typora — a markdown editor](https://typora.io/) 来书写的，没有进行额外的设置—— Typora 的功能是所写即所得，不用添加额外预览功能。如果需要查看原生格式可以使用快捷键 `Command + /` (MacOS) 或者 `Ctrl + /` (Windows)。



# $\rm I$. 基本格式语法

在进行常规书写的时候，常用的格式包括 `Heading`——可以用描述标题内容， 有序和无序列表，斜体，加粗，表格，代码块等格式。

## 1.1 Heading

`Heading` 的标签模式和 HTML 中 `<h>` 标签具有同样功能。HTML 中通过添加数字来表示 `heading` 等级，在 markdown 中通过 `#` 的个数表示同样的功能——例如上面的 `# 基本格式语法` 就是 `H1` 等级的 `heading`，而上面的 `## Heading` 就是 `H2` 等级的 `heading`。常见的语法如下：

```markdown
# h1 的 heading
## h2 的 heading
### h3 的 heading
#### h4 的 heading
##### h5 的 heading
###### h6 的 heading
```

下面是在 [MacDown:  open source Markdown editor for macOS](https://macdown.uranusjr.com/) 中的书写和表现对比：

![image-20181226225518677](https://ws2.sinaimg.cn/large/006tNbRwgy1fykjfe6yoqj30ua0iqtbe.jpg)

## 1.2 常见文字格式

常见的文字格式就是分别为斜体、加粗，这两个可以通过添加 `*` 或者 `_` 来进行调整文字格式。其中一个 `*` 或者 `_` 是将字体变为斜体，添加两个 `*` 或者 `__` 可以将字体调整为粗体，下面是语法演示：

```markdown
*字体变为斜体*
**字体加粗**

_字体变为斜体_
__字体加粗__
```

以上内容得到的效果如下：

*字体变为斜体*
**字体加粗**

## 1.3 列表

列表分为有序列表和无序列表两种形式，其主要的书写方式存在差异。有序列表需要使用**数字**加**点号**及**空格**来表示——`1. ` ；而无序列表可以通过**星号**或者**减号**加**空格**来表示——`* ` 或者 `-  ` 。下面是语法演示：

```markdown
1. 第一个有序列表 list
2. 第二个有序列表 list
3. 第三个有序列表 list


* 第一个无序列表 list
* 第二个无序列表 list
* 第三个无序列表 list

- 第一个无序列表 list
- 第二个无序列表 list
- 第三个无序列表 list
```

得到的效果如下：

1. 第一个有序列表 list
2. 第二个有序列表 list
3. 第三个有序列表 list


* 第一个无序列表 list
* 第二个无序列表 list
* 第三个无序列表 list

## 1.4 表格

在 markdown 中同样可以插入表格内容，插入的方式如下：

```markdown
| 第一列 | 第二列 |
| ------ | ------ |
| 内容一 | 内容二 |
```

得到的小如过下：

| 第一列 | 第二列 |
| ------ | ------ |
| 内容一 | 内容二 |

上面的效果是没有进行格式调整，如果需要对内容的对齐方式调整可以通过在第二行中添加冒号（`:`）来说明对齐方式：

```markdown
| 第一列左对齐 | 第二列居中齐 | 第三列有对齐 |
| :--------- | :--------: | ---------: |
| 内容一      | 内容二      |   内容三    |
```

下面是得到的效果，分别对第一列进行做对齐，第二列居中对齐和第三列右对齐处理：

| 第一列左对齐 | 第二列居中齐 | 第三列有对齐 |
| :----------- | :----------: | -----------: |
| 内容一       |    内容二    |       内容三 |

## 1.5 代码

代码可以分为行内代码和行间代码，行内的代码可以表示是一个简单的表达式或者语句。如果是需要在行内插入代码可以通过 \`\` （即**反引号**，一般是 Tab 键上面的那个键或者说是在数字 1 之前那个键），在反引号内书写内容；当需要添加大量的代码块内容时，那么就需要使用三个反引号换行书写内容之后换行添加另三个反引号——注意可以在第一行中添加  `{}` 以及语言类型来说明是哪种语言的代码，⚠️这点在 Rstudio 中使用 `RMD` 文件，即 `R` 的 markdown 文件中尤其重要。演示如下：

```markdown
这个是一个行内的代码 `python [option] filename.py`，下面是一个行间代码块：

​```{R}
# 加载 test.csv 文件为 data.frame
df <- read.csv("./test.csv")
​```
```

这个是一个行内的代码 `python [option] filename.py`，下面是一个行间代码块：
```{R}
# 加载 test.csv 文件为 data.frame
df <- read.csv("./test.csv")
```

## 1.6 其他格式

在书写 markdwn 的过程中，可能还需要进行添加一个链接、图片等内容。当然可以通过写 HTML 的方式来进行添加，需要以 markdown 的语法来进行书写的话可以通过 `[]()` 的格式来添加链接，`![]()` 来添加一个图片——注意图片可以是本地的文件也可以是一个图片链接，格式语法如下：

```markdown
[这个是 Udacity 的中文网站链接](https://cn.udacity.com)

![这个是 Udacity 本地文件](../img/udacity_logo.svg)
![这个是 Udacity 图片网页链接](https://classroom.udacity.com/images/word-mark-78490.svg)
```

[这个是 Udacity 的中文网站链接](https://cn.udacity.com)
![这个是 Udacity 本地文件](../img/udacity_logo.svg)

# $\rm II$. 数学表达式

markdown 的数学表达式的书写，是遵循了 `Latex` 的常用语法格式。但是因为某些网站支持了 markdown 但是并不支持 `Latex` ，所以看起来文档出现很怪异的现象（例如现在看见的 GitHub 上，可能为看见 \$\$ 等标识符）。

## 2.1 单行与多行表达式

数学表达式分为两类：**单行表达式** 和 **多行表达式**。两者的差异主要在于使用了几个 `$` 标识符，此外多行表达式每行 `\\`结尾，每个元素 `&`分隔。下面演示单行表达式和多行表示：

```latex
这个是单行的质能方程 $E=mc^2$，下面是一个多行的事件概率表示：
$$
\begin{cases}
p=0, & x=不可能事件 \\
0 \lt p \lt 1, & x=随机事件 \\
p=1, & x=必然事件\\
\end{cases}
$$
```

这个是单行的质能方程 $E=mc^2$，下面是一个多行的事件概率表示：
$$
\begin{cases}
p=0, & X=不可能事件 \\
0 \lt p \lt 1, & X=随机事件 \\
p=1, & X=必然事件\\
\end{cases}
$$

## 2.2 上标和下标

在书写过程中可能会遇见上标和小标的可能行，上标需要使用 `^` ，下标需要 `_` 。如果遇到使用过多内容的上下标处理，那么就需要使用 `{}` 将所有内容进行包裹，格式如下：

```latex
$f(x)=1/(1+e^{-(b_0+b_1*x)})$
```

这个是一个 Sigmoid 函数和一元一次函数构成的复合函数 $f(x)=1/(1+e^{-(b_0+b_1*x)})$。



**Note：**

当然 `Latex` 有更优雅的语法可以使用，例如上面的表达式可以使用`\frac{}{}` 来表示 $f(x)=\frac{1}{1+e^{-(b_0+b_1*x)}}$。更多的方式，可以查看一下 `Latex` 语法[^3]

## 2.3 其他常见标识符

|    代码    |   效果   | 意义     |
| :--------: | :------: | -------- |
|  `$\sum$`  |  $\sum$  | 求和     |
|  `$\leq$`  |  $\leq$  | 小于等于 |
|  `$\geq$`  |  $\geq$  | 大于等于 |
|  `$\neq$`  |  $\ne$   | 不等于   |
|  `$\gt$`   |  $\gt$   | 大于     |
|  `$\lt$`   |  $\lt$   | 小于     |
|  `$\mu$`   |  $\mu$   |          |
| `$\sigma$` | $\sigma$ |          |

## 2.4 详细其他参考内容

### 2.4.1 希腊字符

| 代码 | 效果 |
| :--: | :--: |
|   `$\alpha$`   |  $\alpha$    |
|   `$\Alpha$`   |  $\Alpha$    |
|`$\beta$`      |$\beta$      |
|`$\Beta$`      |$\Beta$      |
|`$\gamma$`      |$\gamma$      |
|`$\Gamma$`      |$\Gamma$      |
|`$\delta$`|$\delta$|
|`$\Delta$`|$\Delta$|
|`$\epsilon$`|$\epsilon$|
|`$\Epsilon$`|$\Epsilon$|
|`$\zeta$`|$\zeta$|
|`$\Zeta$`|$\Zeta$|
|`$\eta$`|$\eta$|
|`$\Eta$`|$\Eta$|
|`$\theta$`      |$\theta$      |
|`$\Theta$`      |$\Theta$      |
|`$\iota$`|$\iota$|
|`$\Iota$`|$\Iota$|
|`$\kappa$`|$\kappa$|
|`$\Kappa$`|$\Kappa$|
|`$\lambda$`|$\lambda$|
|`$\Lambda$`|$\Lambda$|
|`$\mu$`|$\mu$|
|`$\Mu$`|$\Mu$|
|`$\nu$`|$\nu$|
|`$\Nu$`|$\Nu$|
|`$\xi$`|$\xi$|
|`$\Xi$`|$\Xi$|
|`$\omicron$`|$\omicron$|
|`$\Omicron$`|$\Omicron$|
|`$\pi$`|$\pi$|
|`$\Pi$`|$\Pi$|
|`$\Rho$`|$\Rho$|
|`$\Rho$`|$\Rho$|
|`$\sigma$`|$\sigma$|
|`$\Sigma$`|$\Sigma$|
|`$\tau$`|$\tau$|
|`$\Tau$`|$\Tau$|
|`$\upsilon$`|$\upsilon$|
|`$\Upsilon$`|$\Upsilon$|
|`$\phi$`|$\phi$|
|`$\Phi$`|$\Phi$|
|`$\chi$`|$\chi$|
|`$\Chi$`|$\Chi$|
|`$\psi$`|$\psi$|
|`$\Psi$`|$\Psi$|
|`$\omega$`|$\omega$|
|`$\Omega$`|$\Omega$|

### 2.4.2 集合与比较

| 代码 | 效果 | 意义 |
| :--: | :--: | :--: |
|`$\not\subset$`      |$\not\subset$      | 不包含于 |
|`$\subset$`|$\subset$|子集，包含于|
|`$\supset$`|$\supset$|超集|
|`$\subseteq$`|$\subseteq$|真子集|
|`$\subseteq$`|$\subseteq$||
|`$\emptyset$`|$\emptyset$|空集|
|`$\in$`|$\in$|属于|
|`$\notin$`|$\notin$|不属于|
|`$\bigcup$`|$\bigcup$|并集|
|`$\bigcap$`|$\bigcap$|交集|
|`$\mathbb{R}$`|$\mathbb{R}$|实数集|
|`$\not$`|$\not$|非|
|`$\bigvee$`|$\bigvee$|逻辑或|
|`$\bigwedge$`|$\bigwedge$|逻辑与|
|`$\nleq$`|$\nleq$|不小于等于|
|`$\ngeq$`|$\ngeq$|不大于等于|
|`$\approx$`|$\approx$|约等于|
|`$\equiv$`|$\equiv$|恒等于|
|`$\infty$`|$\infty$|无穷|
|`$\sim$`|$\sim$|相关符号，例如正太分布 $X \sim N(\mu,\sigma^2)$|

### 2.4.3 矩阵

使用 `\begin{matrix}`开头及`\end{matrix}`结尾，每行 `\\`结尾，每个元素 `&`分隔。此外向量的表示是 `$\vec{}$`，例如 $\vec{a}$

```latex
$$
\begin{matrix}
  1 & 0 & 0 \\
  0 & 1 & 0 \\
  0 & 0 & 1 \\
\end{matrix}
$$

$$
\begin{pmatrix}
  1 & 0 & 0 \\
  0 & 1 & 0 \\
  0 & 0 & 1 \\
\end{pmatrix}
$$

$$
\begin{bmatrix}
  1 & 0 & 0 \\
  0 & 1 & 0 \\
  0 & 0 & 1 \\
\end{bmatrix}
$$

$$
\begin{Bmatrix}
  1 & 0 & 0 \\
  0 & 1 & 0 \\
  0 & 0 & 1 \\
\end{Bmatrix}
$$

$$
\begin{vmatrix}
  1 & 0 & 0 \\
  0 & 1 & 0 \\
  0 & 0 & 1 \\
\end{vmatrix}
$$

$$
\begin{Vmatrix}
  1 & 0 & 0 \\
  0 & 1 & 0 \\
  0 & 0 & 1 \\
\end{Vmatrix}
$$
```

$$
\begin{matrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{matrix}
$$
$$
\begin{pmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{pmatrix}
$$
$$
\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{bmatrix}
$$
$$
\begin{Bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{Bmatrix}
$$
$$
\begin{vmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{vmatrix}
$$
$$
\begin{Vmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{Vmatrix}
$$

### 2.4.4  数学运算符号
| 代码 | 效果 | 意义 |
| :--: | :--: | :--: |
|`$\times$`|$\times$|乘法|
|`$\div$`|$\div$|除法|
|`$\pm$`|$\pm$|正负号|
|`$\mp$`|$\mp$|负正号|
|`$\cdot$`|$\cdot$|点乘|
|`$\ast$`|$\ast$|星乘|
|`$\frac{}{}$`|$\frac{1}{2}$|分数表示法|
|`$\log$`|$\log$|对数运算|
|`$\ln$`|$\ln$|自然对数运算|
|`$\sin$`|$\sin$|正弦函数|
|`$\sum$`|$\sum$|累加|
|`$\prod$`|$\prod$|累乘|
|`$\coprod$`|$\coprod$|余积|
|`$\int$`|$\int$|积分|
|`$\iint$`|$\iint$|二次积分|
|`$\oint$`|$\oint$|曲线积分|
|`$\lim$`|$\lim$|极限|
|`$\partial$`|$\partial$|导数|
|`$\nabla$`|$\nabla$|梯度|
|`$\sqrt$`|$\sqrt{ax+b}$|求平方根|
|`$\bigotimes$`|$\bigotimes$|克罗内克积|
|`$\bigoplus$`|$\bigoplus$|异或|
|`$\bigodot$`|$\bigodot$|加运算|
|`$\because$`|$\because$|因为|
|`$\therefore$`|$\therefore$|所以|
|`$\forall$`|$\forall$|任意|
|`$\exists$`|$\exists$|存在|

### 2.4.5 其他类型
| 代码 | 效果 | 意义 |
| :--: | :--: | :--: |
|`$\ldots$`|$\ldots$|底部省略号|
|`$\cdots$`|$\cdots$|中部省略号|
|`$\hat$`|$\hat{y}$||
|`$\check$`|$\check{y}$||
|`$\breve$`|$\breve{y}$||
|`$\circ$`|$90^\circ$|可以用于表示度数|
|`$\overline$`|$\overline{a+b+c}$|用于表示平均值|
|`$\underline$`|$\underline{a+b}$||
|`$\uparrow$`|$\uparrow$||
|`$\Uparrow$`|$\Uparrow$||
|`$\backslash$`|$\backslash$||
|`$\Updownarrow$`|$\Updownarrow$||
|`$\Rightarrow$`|$\Rightarrow$||
|`$\Longleftarrow$`|$\Longleftarrow$||
|`$\overbrace$`|$\overbrace{a + b}$|上方括号，见下方示例|
|`$\mid$`|$\mid$|竖线|
|`$\lbrace \rbrace$`|$\lbrace \rbrace$|花括号|

示例：

* `$\overbrace{a+\underbrace{b+c}_{1.0}+d}^{2.0}$` 结果为 $\overbrace{a+\underbrace{b+c}_{1.0}+d}^{2.0}$

* 上花括弧命令：\overbrace{公式}{说明}

* 下花括弧命令：\underbrace{公式}_{说明}

  例如：`$\underbrace{a+\overbrace{b+\dots+b}^{m\mbox{ 个}}}_{20\mbox{ 个}}$`显示为：$\underbrace{a+\overbrace{b+\dots+b}^{m\mbox{ 个}}}_{20\mbox{ 个}}$

### 2.4.6 特殊格式

1. 堆积符号

   - `\stacrel{上位符号}{基位符号}` 基位符号大，上位符号小
   - `{上位公式\atop 下位公式}` 上下符号一样大
   - `{上位公式\choose 下位公式}` 上下符号一样大；上下符号被包括在圆弧内

   示例 `$\vec{x}\stackrel{\mathrm{def}}{=}{x_1,\dots,x_n}\\ {n+1 \choose k}={n \choose k}+{n \choose k-1}\\ \sum_{k_0,k_1,\ldots>0 \atop k_0+k_1+\cdots=n}A_{k_0}A_{k_1}\cdots $` 结果为 $\vec{x}\stackrel{\mathrm{def}}{=}{x_1,\dots,x_n}\\ {n+1 \choose k}={n \choose k}+{n \choose k-1}\\ \sum_{k_0,k_1,\ldots>0 \atop k_0+k_1+\cdots=n}A_{k_0}A_{k_1}\cdots$

2. 定界符

   通过 `\big` , `\Big`, `\bigg`,  `\left`, `\right` 等进行控制， 例如 `$()\big(\big)\Big(\Big)\bigg(\bigg)\Bigg(\Bigg)$`，结果为$()\big(\big)\Big(\Big)\bigg(\bigg)\Bigg(\Bigg)$。此外示例

   `$\left(x\right) \left(x^{y^{\scriptstyle z}}\right)$` 结果为 $\left(x\right) \left(x^{y^{\scriptstyle z}}\right)$

3. 占位宽度

   - `\qquad` 表示两个 quad 空格 `$a \qquad b $` 结果显示为：$a \qquad b $
   - `\quad` 表示一个 quad 空格 `$a \quad b$` 结果显示为 $a \quad b$
   - 一个空格 `$a\ b$` 表示 1/3m宽度，结果显示为：$a\ b$
   - `;` 表示 `$a\;b$` 占 2/7m宽度，结果显示为：$a\;b$
   - `,` 表示 1/6m宽度`$ a\,b$`, 显示为：$ a\,b$
   - 没有占位控制，`$ab$`, 显示为：$ab$
   - `!` 表示紧贴缩进1/6m宽度`$a\!b$`, 显示为：$a\!b$

**Note:** 目前还有其他格式控制，例如 `\display`, `\textstyle`, `\scripstyle` 等[^4]

# $\rm A$. 参考

[^1]: [Markdown 维基百科](https://zh.wikipedia.org/wiki/Markdown) 
[^2]: [教程-MarkDown](http://www.markdown.cn/)

​	markdown 中文语法详细内容，对应了 [Daring Fireball: Markdown Syntax Documentation](https://daringfireball.net/projects/markdown/syntax) 的内容

[^3]: [Markdown 数学公式](http://blog.lisp4fun.com/2017/11/01/formula)
[^4]: [Display style in math mode - Overleaf, Online LaTeX Editor](https://www.overleaf.com/learn/latex/Display_style_in_math_mode) 
[^5]: [How To Write Mathematical Equations, Expressions, and Symbols with LaTeX: A cheatsheet.](https://www.authorea.com/users/77723/articles/110898-how-to-write-mathematical-equations-expressions-and-symbols-with-latex-a-cheatsheet)

​	罗列了怎么书写数据表达式，并且有相关的分类