# LaTex学习笔记




# LaTeX

## 1.latex的结构

```latex
% 导言区
\documentclass{article} %一种文档类，也可以是book,report,letter
\usepackage{ctex}	%使用中文包
\title{My First Document}	%文章的标题
\author{Y tq}	%文章的作者
\date{\today}	%文档的时间，today表示今天


% 正文区（文稿区）
\begin{document} %环境名称
	\maketitle	%输出标题,letter类没有maketitle
	Hello World!
	
	%空一行表示产生新的段落,多个空行看做一个空行,\\表示换行
	Let $f(x)$ be defined by the formula
	$$f(x)=3x^2+x-1$$.
	% $ $内表示行内公式 $$ $$表示行公式
\end{document}
```

eg:

```latex
\documentclass{article}
\usepackage{ctex}


\title{\heiti 第一次使用latex}
\author{\kaishu 于天祺}
\date{\today}

\begin{document}
	\maketitle
	Hello World \LaTeX.
	
	Let $f(x)$ be defined by the formula
	$$f(x)=3x^2+x-1$$.
	
	勾股定理可以用现代语言表述如下：
	
	直角三角形斜边的平方等于两腰的平方和。
	
	可以用符号语言表述为：设直角三角形 $ABC$, 其中 $\angle C=90^\circ$,则有：
	\begin{equation}
		AB^2 = BC^2 + AC^2.
	\end{equation}
	
\end{document}
```



## 2.字体设置

```latex
\documentclass[10pt]{article}

\usepackage{ctex}
\newcommand{\myfont}{\textit{\textbf{\textsf}}}

\begin{document}
	%字体族设置（罗马字体，无衬线字体，打字机字体）
	\textrm{Roman Family} \textsf{Sans Serif} \texttt{Typerwriter Family}
	%这种是声明大括号内的字体
	\rmfamily Roman Family {\sffamily Sans Serif} {\ttfamily Typewriter Family}
	%这种是声明命令之后的字体，大括号对文本分组限定命令作用的范围
	
	%字体系列设置（粗细，宽度）
	\textmd{Medium Series} \textbf{Boldface Series}
	
	{\mdseries Medium Serises} {\bfseries Boldface Series}
	%字体形状设置（直立，斜体，伪斜体，小型大写）
	\textup{Upright Shape} \textit{Italic Shape}
	\textsl{Slanted Shape} \textsc{Small Caps Shape}
	
	{\upshape Upright Shape} {\itshape Italic Shape} {\slshape Slanted Shape} {\scshape Small Caps Shape}
	
	%中文字体 \quad是空格
	{\songti 宋体} \quad {\heiti 黑体} \quad {\fangsong 仿宋} \quad {\kaishu 楷书}
	
	中文字体的\textbf{粗体}与\textit{斜体}
	
	%字体大小
	{\tiny				hello}\\
	{\scriptsize		hello}\\
	{\footnotesize		hello}\\
	{\small				hello}\\
	{\normalsize		hello}\\
	{\large				hello}\\
	{\Large				hello}\\
	{\LARGE				hello}\\
	{\huge				hello}\\
	{\Huge				hello}\\
	%双斜杠是换行
	
	%中文自豪设置命令
	\zihao{-0} 你好!
	
\end{document}
```

## 3.文档的基本结构

```latex
\documentclass{article}

\usepackage{ctex}

\begin{document}
	
	%构建提纲
	\section{引言}
	\section{试验方法}
	
	\chapter{绪论}			%chapter（章节）只在book类型中有
	\section{研究的目的和意义}
	\section{国内外研究现状}
	\subsection{国内研究现状}
	\subsection{国外研究现状}
	\section{研究内容}
	\section{研究方法与技术路线}
	\subsection{研究内容}
	\subsection{技术路线}
	\chapter{试验与结果分析}
	\section{引言}
	\section{试验方法}
	\section{试验结果}
	\subsection{数据}
	\subsection{图表}
	\subsubsection{试验条件}
	\subsubsection{试验过程}
	\subsection{结果分析}
	\section{结论}
	\section{致谢}
	
\end{document}
```

## 4.特殊字符

```latex
\documentclass{article}
\usepackage{ctex}
\begin{document}
	%空白字符 
	\quad  \+空格
	%待添加。。。
\end{document}
```

## 5.插入图片

```latex
\documentclass{article}
\usepackage{ctex}
\usepackage{graphicx}		%使用此宏包实现插图
\graphicspath{{figures/},{pics/}} %图片在当前路径下的figure目录，指定图片搜索路径,可以分组！！一定是两个大括号
\begin{document}
	\includegraphics[选项]{文件名}
	% 格式 EPS,PDF,PNG,JPEG,BMP
	选项：
	scale=0.3 缩放因子
	height=2cm 图像高度
	width=2cm 图像宽度
	height=0.1\textheight	原文本高度的0.1倍的高度
	width=0.2\textwidth
	angle=-45 旋转角度
	参数间用逗号分隔
	
\end{document}
```

## 6.表格

```latex
\documentclass{article}
\usepackage{ctex}
\begin{document}
		\begin{tabular}{|l||c|c|c|p{1.5cm}|} %l,c,r，左，中，右，对齐方式，|添加分隔线p产生指定宽度的表列，会自动换行
		\hline
		姓名 & 语文 & 数学 & 外语 & 备注\\
		\hline \hline
		张三 & 87 & 100 & 93 & 优秀\\
		\hline
		李四 & 75 & 64 & 52 & 补考另行通知\\
		\hline
		王二 & 80 & 82 & 78 & \\
		\hline
	\end{tabular}
\end{document}
```

## 7.浮动体

相当于在文字流中浮动

```latex
\documentclass{article}
\usepackage{ctex}
\usepackage{graphicx}
\begin{document}
	爆炒溜肥肠成本见图\ref{fig-fwih}
	\begin{figure}[htbp]
		\centering	%使浮动内容居中
		\includegraphics[scale=0.3]{feichang}
		\caption{爆炒肥肠}\label{fig-fwih} %图片设置标题，也可适用于table中
	\end{figure}
	
	当然，也可以在\LaTeX{}中使用表\ref{tab-score}
	\begin{table}[htbp]
		\centering
		\caption{考试成绩单}\label{tab-score}
		\begin{tabular}{|l||c|c|c|p{1.5cm}|} %l,c,r，左，中，右，对齐方式，|添加分隔线p产生指定宽度的表列，会自动换行
		\hline
		姓名 & 语文 & 数学 & 外语 & 备注\\
		\hline \hline
		张三 & 87 & 100 & 93 & 优秀\\
		\hline
		李四 & 75 & 64 & 52 & 补考另行通知\\
		\hline
		王二 & 80 & 82 & 78 & \\
		\hline
	\end{tabular}
	\end{table}
	% figure 使图片浮动，tabular使表格浮动
\end{document}
```

## 8.数学公式初步

LaTeX将排版内容分为文本模式和数学模式，文本模式用于普通文本排版，数学模式用于数学公式排版

*1.行内公式*

​	1.$ a+b=b+a $

2. \(a+b=b+a\)
3. math环境：\begin{math}a+b=b+a\end{math}

*2.上下标*：

1. $3x^2-x+2=0,3x^{20}-x+2=0,3x^{a+b}$
2. $a_0+a_1+a_{3+2x^2}$

*3.希腊字母*

$\alpha,\beta,\gamma,\epsilon,\pi,\omega,\Gamma,\Delta$

$\Theta,\Pi,\Omega$

$\alpha^3+\beta^2+\gamma$

*4.数学函数*

1. $\log,\log^2_3,\log_3^2$ 
2. $\sin,\cos,\sin^2x+\cos^2x=1$
3. $\arcsin,\arccos$
4. $\ln$
5. $\sqrt2,\sqrt{x^2+y^2},\sqrt{2+\sqrt2},\sqrt[4]3$
6. $3/4,\frac34,\frac{x}{x^2+x+1},\frac{\sqrt{x-1}}{\sqrt{x+1}},\frac{1}{1+\frac{1}{x}},\sqrt{\frac{x}{x^2+x+1}}$

*5.行间公式*

​	$$ a+b=b+a $$

\[a+b=b+a\] 		(注意：中括号左右都有反斜杠！)

\begin{displaymath}1+2=3\end{displaymath}

*6.自动编号公式*

交换律公式：\ref{eq:commutative}

\begin{equation}

​	a+b=b+a	\label{eq:commutative}(标签)

\end{equation}

## 9.数学矩阵

```latex
\documentclass{article}
\usepackage{ctex}
\usepackage{amsmath}

\begin{document}
	% 矩阵环境，&符号分隔列，\\符号分隔行
	\[
	\begin{matrix}
		0&1\\
		1&0
	\end{matrix}\qquad
	\begin{pmatrix}
		0&1\\
		1&0
	\end{pmatrix}\qquad
	\begin{bmatrix}
	0&1\\
	1&0
	\end{bmatrix}\qquad
	\begin{Bmatrix}
	0&1\\
	1&0
	\end{Bmatrix}\qquad
	\begin{vmatrix}
	0&1\\
	1&0
	\end{vmatrix}\qquad
	\begin{Vmatrix}
	0&1\\
	1&0
	\end{Vmatrix}\qquad
	\]
	\[
	A = \begin{pmatrix}
		a_{11}^2 & a_{12}^2 &a_{13}^2 \\
		0 & a_{22} & a_{23} \\
		0 & 0 & a_{33}
	\end{pmatrix}
	\]
	
	%矩阵中常用省略号 \dots,\vdots,\ddots
	\[
	A = \begin{bmatrix}
	a_{11} & \dots &a_{1n} \\
	&\ddots & \vdots \\
	0 & & a_{nn}
	\end{bmatrix}_{n \times n}
	\]
	
	%分块矩阵（矩阵嵌套）
	\[
		\begin{pmatrix}
			\begin{matrix}
				1&0\\0&1
			\end{matrix} & \text{\Large 0}\\
			\text{\Large 0} & \begin{matrix}
			1&0\\0&-1
			\end{matrix}
		\end{pmatrix}
	\]
	\[
	\begin{pmatrix}
		a_{11} & a_{12} & \cdots &a_{1n}\\
		&a_{22}& \cdots & a_{2n}\\
		&	   & \ddots & \vdots\\
		\multicolumn{2}{c}{\raisebox{1.3ex}[0pt]{\Huge 0}}
		&	   &a_{nn}	
	\end{pmatrix}
	\]
	% 跨列省略号：\hdotsfor{columns}
	\[
	\begin{pmatrix}
		1 & \frac 12 & \dots & \frac 1n\\
		\hdotsfor{4}\\
		m & \frac m2 & \dots & \frac mn
	\end{pmatrix}
	\]
	
	%行内小矩阵 (smallmatrix) 环境 
	复数 $z = (x,y)$ 也可以用矩阵
	\begin{math}
		\left(% 需要手动加上左括号
		\begin{smallmatrix}
		x & -y \\ y & x
		\end{smallmatrix}
		\right)%
	\end{math}来表示。
	
	% array环境（类似于表格环境tabular）
	\[
	\begin{array}{r|r}
	\frac12 & 0 \\
	\hline
	0 & -\frac abc \\
	
	\end{array}
	\]
%	% 用array环境构造复杂矩阵
%	\[
%	% @{<内容>}-添加任意内容，不占表项技术
%	% 此处添加一个负值空白，表示向左移 -5pt的距离
%	\begin{array}{c@{\hspace{-5pt}}l}
%	%第一行，第一列
%	\left(
%	\begin{array}{ccc|ccc}
%	a & \cdots & a & b & \cdots & b\\
%	& \ddots & \vdots & \vdots & \\
%	&		 & a & b \\ \hline
%	& 		 &   & \vdots & & \vdots\\
%	\multicolumn{2}{c|}{\raisebox{2ex}[0pt]{\Huge 0}}
%	& c & \cdots & c
%	\end{array}
%	\right)
%	\end{array}
%	
%	
%	\]
	
\end{document}
```



## 10.数学公式的多行公式

```latex
\documentclass{article}
\usepackage{ctex}
\usepackage{amsmath}
\usepackage{amssymb}

\begin{document}
	\begin{gather}
		%带编号,\notag组织编号
		a+b = b+a\\
		ab = ba \notag \\
		a^b
	\end{gather}
	
	\begin{gather*}
		%不带编号
		3+5=8\\
		3 \times 5 = 15
	\end{gather*}
	%align 和 aligh* 环境(用&进行对齐,&的位置代表公式对齐的位置！)
	\begin{align}
		x &=t + \cos t + 1\\
		y &=2\sin t
	\end{align}
	\begin{align*}
		x &= t & x &= \cos t & x &= t \\
		y &= 2t & y &= \sin(t+1) & y &= \sin t
	\end{align*}
	% split 环境 （对齐采用 align 环境的方式，编号在中间）
	\begin{equation}
		\begin{split}
			\cos 2x &= \cos^2 x - \sin^2 x \\
			&= 2\cos^2 x - 1
		\end{split}
	\end{equation}
	% cases环境
	% 每行公式中使用 & 分隔为两部分，
	% 通常表示值和后面的条件
	\begin{equation}
	D(x) = \begin{cases}
	1, & \text{如果 } x \in \mathbb{Q}; \\
	0, & \text{如果 } x \in \mathbb{R}\setminus \mathbb{Q}.
	\end{cases}
	% 一定要使用text命令实现文本模式，实现中文排版，
	\end{equation}
	
	
\end{document}
```



## 11.自定义命令和环境

```latex
\newcommand<命令>[<参数个数>][<参数默认值>]{<具体定义>}
eg: \newcommand\PRC{People`s Republic of \emph{China}}
% \newcommand也可以使用参数
% 参数个数可以从1到9，使用时用 #1,#2,......,#9 表示
eg:
\newcommand\lovexs[2]{#1 喜欢 #2}
\newcommand\hatedby[2]{#2 不受 #1 喜欢}
\loves{猫}{鱼}
\hatedby{狗}{萝卜}
% \newcommand的参数也可以有默认值
% 指定参数格式的同时指定了首个参数的默认值，那么这个命令的
% 第一个参数就成为可选的参数(要使用中括号指定)
eg:
\newcommand[3][喜欢]{#2#1#3}
% \renewcommand-重新定义已有的命令
% 与\newcommand 命令作用和用法相同，但只能用于已有的命令
% \renewcommand<命令>[<参数个数>][<参数默认值>]{<具体定义>}
eg:
\renewcommand\abstractname{内容简介}
% 该命令会被abstract环境自动调用

%定义和重新定义环境
% \newenvironment{<环境名称>}[<参数个数>][<首参数默认值>]{<环境前定义>}{<环境后定义>}
% \renewenvironment{<环境名称>}[<参数个数>][<首参数默认值>]{<环境前定义>}{<环境后定义>}
```


