---
title: "LaTeX 基础"
categories:
  - coding
excerpt: "争取用这个做大作业"
tags:
  - LaTeX
last_modified_at: 2020-06-21T30:21:32-22:02
---

本文是根据 [Overleaf](www.overleaf.com) 上的 [<i>Learn $\LaTeX$ in 30 minutes</i>](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes) 指导教程写成的学习笔记。

由于我懒，没有放演示图片进来，要看效果还请自己打开编辑器把代码敲出来编译一下 XD。

还是由于我懒，我也没有写如何搭建 $\LaTeX{}$ 编译环境，想要在电脑上安装 $\LaTeX$ 请移步搜索引擎 XD。不过上文提到的 [Overleaf](www.overleaf.com) 是一个很优秀的可以在线编译 $\LaTeX$ 的网站，倾心推荐。

---

## 一段最简单的 $\LaTeX$ 代码

```LaTeX
\documentclass{article}

\begin{document}

This is my first \LaTeX{} file. This is just a simple example, with no extra parameter or packages included.

\end{document}
```

在以上这段代码中，`\documentclass{article}` 声明了文档的类型（class）。在这个例子中，文件的类型是 `article`，另外还有一些其他的文档类型例如 `book`，`report` 等等。

`\begin{document}` 和 `\end{document}` 标志着文档正文（body）的开始与结束。正文被写在这一对标签之间。

值得一提的是，上面代码中提到 $\LaTeX{}$ 时，并没有直接使用英文单词 LaTeX，而是使用了命令 `\LaTeX{}`，这个命令可以打出错落有致的 $\LaTeX{}$。另外，`\LaTeX` 命令就已经可以打出 $\LaTeX{}$ 了，但由于 $\LaTeX{}$ 命令后的空格会被无视掉，因此单使用 `\LaTeX` 命令会使 $\LaTeX{}$ 符号和后面的文字内容连起来。为了解决这个问题，就需要在命令后加一个花括号，表明命令结束。其实最“正宗”的 $\LaTeX{}$ 应当是正体的，但由于这里 mathjax 渲染的问题，只能显示为斜体，不过也八九不离十了。
## 文档前言

正文之前的内容（如标题、作者、日期）被成为文档的<b>前言（preamble）</b>。上文代码狂中的 `\documentclass{article}` 就是前言的描述之一。还有一些其他常见的前言描述，例如规定字符编码方式、文章题目、作者、日期等。以下是一段添加了一些简单的前言描述之后的代码：

```LaTeX
\documentclass[12pt, letterpaper]{article}
\usepackage[utf8]{inputenc}
\title{My First \LaTeX{} Article}
\author{Richard \thanks{guided by the Overleaf team}}
\date{June 2020}

\begin{document}

\maketitle
Hello, world!

\end{document}
```

其中，`\documentclass[12pt, letterpaper]{article}` 在花括号之前的方括号中写入了一些参数，`12pt` 规定了正文字体大小，`letterpaper` 规定了纸张类型为信纸。一些其他的纸张类型例如 `a4paper`、`legalpaper`。

`\usepackage[utf8]{inputenc}` 规定了文档中字符的编码方式为 UTF-8。使用 UTF-8 编码是一个比较好的选择。

`\title{My First \LaTeX Article}` 规定了文章标题。

`\author{Richard}` 规定了文章的作者。在 `\author{...}` 里可以加上致谢词，致谢词的内容写在 `\thanks{...}` 的花括号里。这一段致谢词会以脚注的形式写在第一页的页脚里。

`\date{June 2020}` 规定了文章的日期为 2020 年 6 月。

要使前言中定义的所有内容都显示到文档中来，必须要在正文的开头加上一句 `\maketitle`。

## 注释

$\LaTeX{}$ 代码注释（comment）写在 `%` 之后。如：

```LaTeX
\begin{document}

Hello, world! % This is the content of the body

\end{document}
```

## 粗体、斜体与下划线

- 粗体：`\textbf{...}`
- 斜体：`\textit{...}`
- 下划线：`\underline{...}`

例如：

```LaTeX
This is a \textbf{bold} word.

This is an \textit{italic} word.

This is an \underline{underlined} word.
```

$\LaTeX$ 中还有一个 `emph{...}` 命令。这个标签会根据上下文所选用的字体样式来自动为花括号内的内容选择不同的字体样式以示强调。例如：

```LaTeX
This is an \emph{emphasized} word.

\textit{This is an \emph{emphasized} word.}

\textbf{This is an \emph{emphasized} word.}
```

上述三句话中，`emphasized` 的样式都不同：第一句是斜体，第二句是正体，第三句是斜体加粗。另外，一些包（package)（例如 Beamer）会改变 `emph{...}` 命令的行为。

## 插入图片

在 $\LaTeX{}$ 中插入图片需要使用 `graphicx` 包。这个包里提供了一些处理图片的新命令，例如 `\includegraphics{...}` 以及 `\graphicspath{...}`。以下是一段插入了图片的代码：

```LaTeX
\documentclass{article}
\usepackage{graphicx}
\graphicspath{ {images/} }

\begin{document}

Below is a picture:

\includegraphics{pic}

\end{document}
```

这段代码中， `\usepackage{graphicx}` 代表我们使用了 `graphicx` 包。`\graphicspath{ {images/} }` 指出了图片的源文件所存放的位置，在这个例子中，图片被存放在名为 `images` 的文件夹中，这个文件夹存在于 `.tex` 源文件所在的目录中。这个例子是相对路径表示法，我们也向花括号内写入绝对路径。绝对路径的表示在 macOS 与 Windows 中有所不同，这里不再赘述。

可以注意到，上面这段代码编译后，图片的显示效果很不佳。我们很多时候需要对图片进行一些额外的处理，例如将图片居中显示、编号，或是添加图片描述。要达成这些功能，我们需要将图片写在 `figure` 环境中。以下是一段写在 figure 环境中的代码：

```LaTeX
\begin{figure}[h]
  \centering
  \includegraphics[width = 0.25 \textwidth]{pic}
  \caption{a picture}
  \label{pic1}

Figure \ref{pic1} is a nice picture.
```

上述代码中，第一行的 `[h]` 代表的是将图片插入到“这里”（here）。`\centering` 使图片居中对齐；`\includegraphics{...}` 将图片插入正文中；`\caption{...}` 为图片添加描述。需要注意的是，$\LaTeX$ 会为图片自动编号。在上述例子中，假定 `pic1` 是文章的第一张图片，它的完整的描述会显示为 "Figure 1: a picture"。

`\label{...}` 与 `\ref{...}` 是一对命令，共同作用。`\label{...}` 给刚刚插入的图片打上了标记，相当于起了一个别名为 `pic1`；`\ref{...}` 则使用别名代指插入的图片，编译后 `\ref{...}` 命令的部分会被转换成图片的编号。在上述例子中，最后一行在 PDF 文件中会显示为 "Figure 1 is a nice picture."

## 项目列表

项目列表（lists）分为<b>无序列表（unordered lists）</b>和<b>有序列表（ordered lists）</b>。

### 无序列表

无序列表写在 `\begin{itemize}` 与 `\end{itemize}` 之间，每一个列表项以 `\item` 开头。例如：

```LaTeX
\begin{itemize}
  \item This is the first unordered item.
  \item This is the second unordered item.
\end{itemize}
```

### 有序列表

有序列表写在 `\begin{enumerate}` 和 `\end{enumerate}` 之间，每一个列表项同样以 `\item` 开头。例如：

```LaTeX
\begin{enumerate}
  \item This is the first ordered item.
  \item This is the second ordered item.
\end{enumerate}
```

## 数学公式

$\LaTeX{}$ 公式分为<b>行内（inline）公式</b>和<b>成段（display）公式</b>。

### 行内公式

行内公式有三种写法： `\( ... \)`，`$ ... $` 以及 `\begin{math} ... \end{math}`。例如：

```LaTeX
This equation \begin{math} E = mc^2 \end{math} is discoverd by Einstein.

This equation $ E = mc^2 $ is discovered by Einstein.

This equation \( E = mc^2 \) is discovered by Einstein.
```

### 成段公式

成段公式有四种定义符，分别是 `\[ ... \]`，`\begin{displaymath} ... \end{displaymath}`，`\begin{equation} ... \end{equation}` 以及 `$$ ... $$`。需要特别提到的是，Overleaf 不建议使用最后一种定义符。另外，equation 环境下的成段公式会被自动编号。

有关具体的数学符号的表示方法，请移步搜索引擎……

## 基础排版

### 摘要

摘要（Abstract）写在文档正文的最开头（通常在 `\maketitle` 以后比较合适）：

```LaTeX
\begin{document}

\begin{abstract}
This is an abstract of this article.
\end{abstract}

\end{document}
```

### 段落与空行

与 markdown 一样，$\LaTeX{}$ 代码在表示分段时，需要敲两下回车键。例如：

```LaTeX
\begin{document}

This is the first paragraph.

This line starts the second parapraph.

\end{document}
```

当然，当我们想特意生成一个空行时，也可选择命令 `\\` 或是 `\newline`。但是，当我们意图「分段」时，我们还是应该使用敲两下回车的方式分段。

### 章与节

|等级|定义符|
|:-:|:-|
|-1|`\part{part}`|
|0|`\chapter{chapter}`|
|1|`\section{section}`|
|2|`\subsection{subsection}`|
|3|`\subsubsection{subsubsection}`
|4|`\paragraph{paragraph}`|
|5|`\subparagraph{subparagraph}`|

注意 `\part{...}` 与 `\chapter{...}` 只能用在 `book` 和 `report` 类型的文章中。

另外，所以的章节都会被 $\LaTeX{}$ 自动编号。如果想要无编号的章节，则需要在花括号之前加一个 `*` ，例如 `\section*{Unnumbered Section}`。

## 表格

以下是一段不加任何边框装饰的“纯”表格代码：

```LaTeX
\begin{center}
\begin{tabular}{c c c}
cell1 & cell2 & cell3 \\
cell4 & cell5 & cell6 \\
cell7 & cell8 & cell9
\end{tabular}
\end{center}
```

上面这段代码中，`\begin{center}` 与 `\end{center}` 这一对定义符使表格居中。`\begin{tabular}` 和 `\end{tabular}` 定义了表格。第二行最后的 `{c c c}` 代表了有三列（columns）。`&` 标志着单元格（cell）与单元格之间的界限，行末的 `\\` 标志着换行。之所以在代码中也换行书写，是为了方便阅读。

表格有两种边框，一种是纵向边框，另一种是横向边框。要添加纵向边框，需要在 `{c c c}` 中添加 `|`，例如我们只需要最左边和最右边的边框，就写 `{|c c c|}`。如果需要每一列都由边框隔开，就写 `{|c|c|c|}`。要添加横向边框，需要在添加边框的地方写 `\hline`。以下是一个既有纵向边框，又有横向边框的例子：

```LaTeX
\begin{center}
\begin{tabular}{|c|c|c|}
\hline
cell1 & cell2 & cell3 \\
\hline
cell4 & cell5 & cell6 \\
\hline
cell7 & cell8 & cell9 \\
\hline
\end{tabular}
\end{center}
```
如果要为表格添加描述以及引用，则需要采用和添加图片类似的方式：

```LaTeX
Table \ref{table:data} is an example of referenced \LaTeX{} elements.

\begin{table}[h]
\centering
\begin{tabular}{||c c c c||}
 \hline
 Col1 & Col2 & Col2 & Col3 \\
 \hline\hline
 1 & 6 & 87837 & 787 \\
 2 & 7 & 78 & 5415 \\
 3 & 545 & 778 & 7507 \\
 4 & 545 & 18744 & 7560 \\
 5 & 88 & 788 & 6344 \\
 \hline
\end{tabular}
\caption{Table to test captions and labels}
\label{table:data}
\end{table}
```
## 目录

直接使用命令 `\tableofcontents` 就可以产生目录了。需要注意的是，无编号章节标题并不会被包括到自动目录里，而需要手动添加。以无编号节标题为例，在 `\section*{Unnumbered Section}` 上一行加一条 `\addcontentsline{toc}{section}{Unnumbered Section}`。以下是在 Overleaf 上的例子：

```LaTeX
\documentclass{article}
\usepackage[utf8]{inputenc}

\title{Sections and Chapters}
\author{Gubert Farnsworth}
\date{ }

\begin{document}

\maketitle

\tableofcontents

\section{Introduction}

This is the first section.

Lorem  ipsum  dolor  sit  amet,  consectetuer  adipiscing  
elit.   Etiam  lobortisfacilisis sem.  Nullam nec mi et
neque pharetra sollicitudin.  Praesent imperdietmi nec ante.
Donec ullamcorper, felis non sodales...

\addcontentsline{toc}{section}{Unnumbered Section}
\section*{Unnumbered Section}

Lorem ipsum dolor sit amet, consectetuer adipiscing elit.  
Etiam lobortis facilisissem.  Nullam nec mi et neque pharetra
sollicitudin.  Praesent imperdiet mi necante...

\section{Second Section}

Lorem ipsum dolor sit amet, consectetuer adipiscing elit.  
Etiam lobortis facilisissem.  Nullam nec mi et neque pharetra
sollicitudin.  Praesent imperdiet mi necante...

\end{document}
```

---

以上就是在 [<i>Learn $\LaTeX$ in 30 minutes</i>](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes) 一文中介绍的简单的 $\LaTeX{}$ 基础技巧。
