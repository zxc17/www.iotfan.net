---
layout: post
title:  "Markdown语法整理"
subtitle: 
showheadline: true
categories: IT
tags: [Markdown, 整理]
---

## 类Select形式标题

``` markdown
This is an H1
=============

This is an H2
-------------
```

## 类Atx形式标题

``` markdown
# 这是一级标题

## 这是二级标题

### 这是三级标题

#### 这是四级标题

##### 这是五级标题

###### 这是六级标题

### 这是三级标题 #####    //
```

>注：允许闭合,且允许后面#号与前面数目不一致，级别以前面#数量为准

## 分割线

``` markdown
***

---

===

- - - - -
```

>注：要求不少于三个

## 区块引用

``` markdown
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
> 
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.
```

等价于

``` markdown
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.
```

引用的区块内也可以嵌套使用其他的 Markdown 语法，包括标题、列表、代码区块等，并且可以在引用中嵌套引用：

``` markdown
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.
```

``` markdown
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.

> ## 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     return shell_exec("echo $input | $markdown_script");
```

效果如下：

----

> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.

> ## 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     return shell_exec("echo $input | $markdown_script");

----

## 列表

**无序列表**使用星号、加号或是减号作为列表标记：

``` markdown
*   Red
*   Green
*   Blue
```

可将上述星号替换为加号或减号，效果完全等价。

**有序列表**则使用数字接着一个英文句点，并且在列表标记上使用的数字并不会影响输出的 HTML 结果：

``` markdown
1.  Bird
2.  McHale
3.  Parish
```

列表项目标记通常是放在最左边，但是其实也可以缩进，最多 3 个空格，项目标记后面则一定要接着至少一个空格或制表符。

要让列表看起来更漂亮，你可以把内容用固定的缩进整理好：

``` markdown
*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.

*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
Suspendisse id sem consectetuer libero luctus adipiscing.
```

如果列表项目间用空行分开，在输出 HTML 时 Markdown 就会将项目内容用 <p> 标签包起来，举例来说：

``` markdown
*   Bird
*   Magic
```

会被转换为：

``` html
<ul>
<li>Bird</li>
<li>Magic</li>
</ul>
```

但是这个：

``` markdown
*   Bird

*   Magic
```

会被转换为：

``` html
<ul>
<li><p>Bird</p></li>
<li><p>Magic</p></li>
</ul>
```

列表项目可以包含多个段落，每个项目下的段落都必须缩进 4 个空格或是 1 个制表符：

``` markdown
1.  This is a list item with two paragraphs. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit. Aliquam hendrerit
    mi posuere lectus.

    Vestibulum enim wisi, viverra nec, fringilla in, laoreet
    vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
    sit amet velit.

2.  Suspendisse id sem consectetuer libero luctus adipiscing.
```

或是

``` markdown
*   This is a list item with two paragraphs.

    This is the second paragraph in the list item. You're
only required to indent the first line. Lorem ipsum dolor
sit amet, consectetuer adipiscing elit.

*   Another item in the same list
```

如果要在列表项目内放进引用，那 > 就需要缩进：

``` markdown
*   A list item with a blockquote:

    > This is a blockquote
    > inside a list item.
```

如果要放代码区块的话，该区块就需要缩进两次，也就是 8 个空格或是 2 个制表符：

``` markdown
*   列表项中包含区块：

	下面是代码区块1：

	``` c
	#include <stdio.h>
	int main()
	{
		printf("hello word!");
		return 0;
	}
	```

	下面是代码区块2：
	
		#include <stdio.h>
		int main()
		{
			printf("hello word!");
			return 0;
		}

*	区块的嵌套：
	
	> This is a blockquote inside a list item.
	>
    > This is the second line.

	1. 这是二级列表。

	    > 这是二级列表内的引用块。
		>
		>``` c++
		>//这是引用块内的代码块
		>printf("hello word!");
		>return 0;
		>```
		>
```

效果如下：

----

*   列表项中包含区块：

	下面是代码区块1：

	``` c
	#include <stdio.h>
	int main()
	{
		printf("hello word!");
		return 0;
	}
	```

	下面是代码区块2：
	
		#include <stdio.h>
		int main()
		{
			printf("hello word!");
			return 0;
		}

*	区块的嵌套：
	
	> This is a blockquote inside a list item.
	>
    > This is the second line.

	1. 这是二级列表。

	    > 这是二级列表内的引用块。
		>
		>``` c++
		>//这是引用块内的代码块
		>printf("hello word!");
		>return 0;
		>```
		>

----

项目列表很可能会不小心产生，避免办法是在句点前面加上反斜杠。如下：

``` markdown
1986\. What a great season.
```

## 代码区块

和程序相关的写作或是标签语言原始码通常会有已经排版好的代码区块，通常这些区块我们并不希望它以一般段落文件的方式去排版，而是照原来的样子显示，Markdown 会用 <pre> 和 <code> 标签来把代码区块包起来。

建立代码区块有两种方式，第一种是简单地缩进 4 个空格或是 1 个制表符，例如，下面的输入：

``` markdown
这是一个普通段落：

    select * from mysql;
    drop database mysql;
    <p>&copy;</p>
```

Markdown 会转换成：

``` html
<p>这是一个普通段落：</p>

<pre><code>
select * from mysql;
drop database mysql;
&lt;p&gt;&amp;copy;&lt;/p&gt;
</code></pre>
```

如上，这中方式的代码区块中每行一阶的缩进（4 个空格或是 1 个制表符），都会被移除。并且，在代码区块里面， & 、 < 和 > 会自动转成 HTML 实体，这样的方式让你非常容易使用 Markdown 插入范例用的 HTML 原始码，只需要复制贴上，再加上缩进就可以了。

第二种是前后各使用三个反引号将代码包括起来，这种方式可以指定代码的语言，以用于代码高亮显示，区块内不需要缩进，如下：

	这是一个普通段落：

	``` sql
	select * from mysql;
	drop database mysql;
	```

预览如下：

----

这是一个普通段落：

``` sql
select * from mysql where host='%';
drop database mysql;
```

----

Markdown 会转换成：

``` html
<p>这是一个普通段落：</p>

<pre><code>select * from mysql;
</code></pre>
```

## 链接

Markdown 支持两种形式的链接语法： *行内式*和*参考式*两种形式。不管是哪一种，链接文字都是用 [方括号] 来标记。

要建立一个**行内式**的链接，只要在方块括号后面紧接着圆括号并插入网址链接即可，如果你还想要加上链接的 title 文字，只要在网址后面，用双引号把 title 文字包起来即可，例如：

``` markdown
This is [an example](http://example.com/ "Title") inline link.

[This link](http://example.net/) has no title attribute.
```

会产生：

``` html
<p>This is <a href="http://example.com/" title="Title">
an example</a> inline link.</p>

<p><a href="http://example.net/">This link</a> has no
title attribute.</p>
```

如果你是要链接到同样主机的资源，你可以使用相对路径：

``` markdown
See my [About](/about/) page for details.
```

**参考式**的链接是在链接文字的括号后面再接上另一个方括号，而在第二个方括号里面要填入用以辨识链接的标记：

``` markdown
This is [an example][id] reference-style link
```

你也可以选择性地在两个方括号中间加上一个空格。

接着，在文件的任意处，你可以把这个标记的链接内容定义出来：

``` markdown
[id]: http://example.com/  "Optional Title Here"
```

链接内容定义的形式为：

- 方括号（前面可以选择性地加上至多三个空格来缩进），里面输入链接文字
- 接着一个冒号
- 接着一个以上的空格或制表符
- 接着链接的网址
- 选择性地接着 title 内容，可以用单引号、双引号或是括弧包着

下面这三种链接的定义都是相同：

``` markdown
[foo]: http://example.com/  "Optional Title Here"
[foo]: http://example.com/  'Optional Title Here'
[foo]: http://example.com/  (Optional Title Here)
```

> 注：部分解释器会忽略单引号包起来的链接 title。

链接网址也可以用尖括号包起来，title 属性也可以放到下一行，并可以加一些缩进，若网址太长的话，这样会比较好看：

``` markdown
[id]: <http://example.com/>  "Optional Title Here"
[id]: http://example.com/longish/path/to/resource/here
    "Optional Title Here"
```

网址定义只有在产生链接的时候用到，并不会直接出现在文件之中。链接辨别标签可以有字母、数字、空白和标点符号，但是并不区分大小写，因此下面两个链接是一样的：

``` markdown
[link text][a]
[link text][A]
```

隐式链接标记功能让你可以省略指定链接标记，这种情形下，链接标记会视为等同于链接文字，要用隐式链接标记只要在链接文字后面加上一个空的方括号，如果你要让 "Google" 链接到 google.com，你可以简化成：

``` markdown
[Google][]
[Google]: http://google.com/

Visit [Daring Fireball][] for more information
[Daring Fireball]: http://daringfireball.net/
```

链接的定义可以放在文件中的任何一个地方，个人偏好直接放在链接出现段落的后面，你也可以把它放在文件最后面，就像是注解一样。

下面是一个参考式链接的范例：

``` markdown
I get 10 times more traffic from [Google] [1] than from
[Yahoo] [2] or [MSN] [3].

  [1]: http://google.com/        "Google"
  [2]: http://search.yahoo.com/  "Yahoo Search"
  [3]: http://search.msn.com/    "MSN Search"
```

如果改成用链接名称的方式写：

``` markdown
I get 10 times more traffic from [Google][] than from
[Yahoo][] or [MSN][].

  [google]: http://google.com/        "Google"
  [yahoo]:  http://search.yahoo.com/  "Yahoo Search"
  [msn]:    http://search.msn.com/    "MSN Search"
```

上面两种写法都会产生下面的 HTML。

``` html
<p>I get 10 times more traffic from <a href="http://google.com/"
title="Google">Google</a> than from
<a href="http://search.yahoo.com/" title="Yahoo Search">Yahoo</a>
or <a href="http://search.msn.com/" title="MSN Search">MSN</a>.</p>
```

参考式的链接其实重点不在于它比较好写，而是它比较好读。使用 Markdown 的参考式链接，可以让文件更像是浏览器最后产生的结果，让你可以把一些标记相关的元数据移到段落文字之外，你就可以增加链接而不让文章的阅读感觉被打断。

Markdown 支持以比较简短的**自动链接**形式来处理网址和电子邮件信箱，只要是用尖括号包起来， Markdown 就会自动把它转成链接。一般网址的链接文字就和链接地址一样，例如：

``` markdown
<http://example.com/>
```

Markdown 会转为：

``` html
<a href="http://example.com/">http://example.com/</a>
```

邮址的自动链接也很类似，只是 Markdown 会先做一个编码转换的过程，把文字字符转成 16 进位码的 HTML 实体，这样的格式可以阻止一部分邮址收集机器人，例如：

``` markdown
<address@example.com>
```

Markdown 会转成：

``` html
<a href="&#x6D;&#x61;i&#x6C;&#x74;&#x6F;:&#x61;&#x64;&#x64;&#x72;&#x65;
&#115;&#115;&#64;&#101;&#120;&#x61;&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;
&#109;">&#x61;&#x64;&#x64;&#x72;&#x65;&#115;&#115;&#64;&#101;&#120;&#x61;
&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;&#109;</a>
```

在浏览器里面，这段字串（其实是 ``<a href="mailto:address@example.com">address@example.com</a>``）会变成一个可以点击的「address@example.com」链接。

## 图片

Markdown 使用一种和链接很相似的语法来标记图片，同样也允许两种样式： 行内式和参考式。

**行内式**的图片语法看起来像是：

``` markdown
![Alt text](/path/to/img.jpg)

![Alt text](/path/to/img.jpg "Optional title")
```

**参考式**的图片语法则长得像这样：

```
![Alt text][id]

[id]: url/to/image  "Optional title attribute"
```

到目前为止， Markdown 还没有办法指定图片的宽高，如果你需要的话，你可以使用普通的 `<img>` 标签。

## 行内代码

如果要标记一小段行内代码，你可以用反引号把它包起来 `` ` `` ，例如：

Use the `` `printf()` `` function

会产生：

``` html
<p>Use the <code>printf()</code> function.</p>
```

如果要在代码区段内插入反引号，你可以用多个反引号来开启和结束代码区段：

``` markdown
``There is a literal backtick (`) here.``
```

代码区段的起始和结束端都可以放入一个空白，起始端后面一个，结束端前面一个，这样你就可以在区段的一开始就插入反引号。

和代码区块类似，在代码区段内，`& < >` 都会被自动地转成 HTML 实体，这使得插入 HTML 原始码变得很容易。

## 强调

Markdown 使用星号（`*`）和底线（`_`）作为标记强调字词的符号，被 `*` 或 `_` 包围的字词会被转成用 `<em>` 标签包围，用两个 `*` 或 `_` 包起来的话，则会被转成 `<strong>`，例如：

``` markdown
*single asterisks*

_single underscores_

**double asterisks**

__double underscores__
```

会转成：

``` html
<em>single asterisks</em>

<em>single underscores</em>

<strong>double asterisks</strong>

<strong>double underscores</strong>
```

可以随便用喜欢的样式，唯一的限制是，用什么符号开启标签，就要用什么符号结束。

强调也可以直接插在文字中间，但是 `*` 和 `_` 符号的两端内侧紧挨的不能是空白，这样的话只会被当成普通的符号。

如果要在文字前后直接插入普通的星号或底线，可以用反斜线。

## 使用反斜线转义特殊字符

Markdown 可以利用反斜杠来将一些在语法中有特殊意义的符号转为本义，常用符号如下:

```
\   反斜线
`   反引号
*   星号
_   底线
{}  花括号
[]  方括号
()  括弧
#   井字号
+   加号
-   减号
.   英文句点
!   惊叹号
```

## 数学公式支持

部分解释器支持TeX格式的数学公式，生成公式的的方式有两种：一种是直接将公式渲染为图片，然后插入原始公式的位置；另一种是将公式预处理后在HTML中由Js解析（需要MathJax.js）。这是一项额外功能，是否支持及实现方式取决于使用的Markdown解释器，这里以[Kramdown][]+[MathJax][]为例。

[Kramdown]: https://kramdown.gettalong.org/converter/latex.html "LaTeX Converter"
[MathJax]: http://docs.mathjax.org/en/latest/start.html "Getting Started"

区块公式使用``$$ <TeX公式> $$``这样的形式声明，公式会被呈现在单独的一行。如：

``` markdown
$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$
```

效果如下：

----

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$

----

行内公式使用``$ <TeX公式> $``这样的形式声明，公式会被插入在文字中间。如：

``` markdown
牛顿-莱布尼茨公式 $ \int_{a}^{b}f(x)dx = F(b)-F(a) $ 揭示了函数的定积分与原函数的关系。
```

效果如下：

----

牛顿-莱布尼茨公式 $ \int_{a}^{b}f(x)dx = F(b)-F(a) $ 揭示了函数的定积分与原函数的关系。

----

点击查看[LaTeX数学符号](http://web.ift.uib.no/Teori/KURS/WRK/TeX/symALL.html)。
<!--\{\{ page.date - 28800 | date: "%Y-%m-%d %H:%M" }}-->

