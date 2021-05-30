## 一、用TexStudio IDE实现LaTeX文档的编写

### 1、新建文件

- 新建文件夹
- 新建文件
- 保存
- 输入命令

```latex
\documentclass{article}		% 表明按论文格式排版

\usepackage{ctex}			% 使用中文包

\begin{document}			% begin与end配合使用
	你好，\LaTeX 。			 % 具体内容
\end{document}
```

- ctrl + 鼠标滚轮进行编辑界面的放大缩小

### 2、编译

![](F:\文档\学习笔记\LaTex\笔记配图\编译.png)

​			第一个按钮为构建并查看，第二个为编译。快捷键：

- F5	Build & View	编译并查看
- F6    Complie    编译
- F7    View    查看



## 二、LaTeX源文件的基本结构

```latex
% 导言区，用于进行全局设置
\documentclass{article}		% 引入文档类（book、report、letter等）

\title{title}	% 文档标题
\author{writer}	% 文档作者
\date{\today}	% 文档编辑时间,\today表示今天

% 正文区（文稿区）
\begin{*环境名称*}		% 环境名称设定为document
	\maketitle		  % 输出标题信息（在letter类中无该命令）
	
	Hello world!		% 内容(文本模式)
						% 空行，用于换行。多个空行被处理为一个空行。写有注释不算空行
	$f(x)$				% “$”包围数学公式(数学模式)，行内公式
	$$ f(x) $$			% 行间公式
	
\end{*环境名称*}		% 一个LaTeX文件有且只能由一个document环境
```



## 三、LaTeX中文处理

### 1、设置		

​		确认”选项-设置“中，“构建-默认编辑器”为XeLaTeX，”编辑器-默认字体编码“为UTF-8。

### 2、自定义命令

```latex
% 导言区
\newcommand\degree{^\circ}	% 自定义\degree命令为右上角的圆圈

% 文档区
$$ \angle C = 90\degree $$
```

### 3、指定中文字体

```latex
\title{\heiti 标题}		% 黑体
\author{\kaishu 作者}		% 楷书
```

### 4、带编号的行间公式

```latex
\begin{equation}
f(x)
\end{equation}
```

### 5、查看宏包

​		cmd中输入texdoc ctex，打开ctex宏包手册，

​		cmd中输入texdoc lshort-zh，打开LaTeX中文简单教程。



## 四、LaTeX字体设置

### 1、字体编码

- 正文字体编码：OT1、T1、EU1等

- 数学字体编码：OML、OMS、OMX等

### 2、字体族

- 罗马字体：笔画起始处有装饰
- 无衬线字体：笔画起始处无装饰
- 打印机字体：每个字符宽度相同，又称等宽字体

```latex
% 字体命令，作用于命令的参数
\textrm{Roman Family}		% 罗马字体
\textsf{Sans Serif Family}	% 无衬线字体
\texttt{Typewriter Family}	% 打印机字体

% 字体声明，作用于后续所有文本
\rmfamily Roman Family			
\sffamily Sans Serif Family		% 更换字体
\ttfamily {Typewriter Family}	% 用大括号进行分组，限定字体申明的范围
```

### 3、字体系列

- 粗细
- 宽度

```latex
% 字体命令
\textmd{Medium Series}
\textbf{Boldface Series}

% 字体申明
\mdseries{Medium Series}
\bfseries{Boldface Series}
```

### 4、字体形状

- 直立
- 斜体
- 伪斜体
- 小型大写

```latex
\textup{Upright Shape}		% 直立形状
\textit{Italic Shape}		% 意大利斜体
\textsl{Slanted shape}		% 伪斜体
\textsc{Small Caps Shape}	% 小型大写

\upshape Upright Shape
\itshape Italic Shape
\slshape Slanted Shape
\scshape Small Caps Shape

% 中文字体设置（需引入ctex宏包）
\songti 宋体
\heiti 黑体
\fangsong 仿宋
\kaishu 楷书

\textbf{粗体}		% 用黑体表示
\textit{斜体}		% 用楷体表示
```

### 5、字体大小

```latex
\documentclass[10pt]{article}	% 设定normal size为10pt。一般只有10、11、12pt

\tiny			Hello		% 相对于normal size的大小
\scriptsize		Hello
\footnotesize	Hello
\small			Hello
\normalsize		Hello
\large			Hello
\Large			Hello
\huge			Hello
\Huge			Hello

% 中文字号设置
\zihao{5}	你好	% {}括号内表示字号。具体查看ctex手册
\zihao{-5}	你好 	% 小五号
```

### 5、自定义字体

```latex
\newcommond{\myfont}{\textbf{textsf{Hello World}}}
```

- LaTeX的重要思想：格式与内容分离

## 五、LaTeX的篇章结构

```latex
\documentclass{ctexart}		% 默认一级标题居中排版
% \documentclass{article}	% 默认小标题靠左排版

% 设置标题格式（参考ctex文档）
\ctexset{
	section = {
		format+ = \zihao{-4} \heiti \raggedright,
		name = {,、},
		number = \chinese{section}
		beforeskip = 1.0ex plus 0.2ex minus .2ex,
		afterskip = 1.0ex plus 0.2ex minus .2ex,
		aftername = \hspace{0pt}
	},
	subsecond = {
		format+ = \zihao{5} \heiti \raggedright,
		name = {,、},
		number = \arabic{subsection}
		beforeskip = 1.0ex plus 0.2ex minus .2ex,
		afterskip = 1.0ex plus 0.2ex minus .2ex,
		aftername = \hspace{0pt}		
	}

}

\begin{document}
	\tableofcontents	% 生成目录

	\chapter{绪论}	% 章节（ctexbook中使用，此时subsubsection不起作用）
	\section{引言}
	\section{正文}
		\subsection{子小节}
			\subsubsection{子子小节}
	\section{结论}
		\\ 		% 反斜杠用于换行，并不另起一段，无缩进
				% 空行另起一段，段首自动缩进2字符
		\par	% 从此处开始产生新段落
\end{document}
```

## 六、LaTeX特殊字符

### 1、空白符号

- 任意多个空格或空行，被识别为一个空格或空行
- 自动缩进，绝不能使用空格代替
- 中文中插入空格不起作用
- 中文与其它字符的间距会自动由XeLaTeX处理
- 禁止使用中文全角空格

### 2、控制符

```latex
\# \$ \% \{ \} \~{} \_{} \^{}
\\				% 换行
\textbackslash	% 输出反斜杠
```

### 3、LaTeX标志符

```latex
\Tex{}	\LaTeX{}	\LaTeXe{}
```

### 4、引号

```latex
`	% 左单引号，输入数字键1左边的'
'	% 右单引号，输入单引号
``	% 连续两个左单引号表示左双引号
''	% 连续两个右单引号表示右双引号
```

### 5、连字符

```latex
-
--
--- % 不同长度的连字符
```

## 七、LaTeX中的插图

```latex
% 导言区：\usepackage{graphicx}
% 语 法：\includegraphics[<选项>]{<文件名>}
% 格 式：EPS,PDF,PNG,JPEG,BMP
\usepackage{graphicx}
\graphicspath{{figures/}}	% 图片在当前目录下的figures目录，不同路径使用大括号分组

% 正文区
\begin{document}
	\includegraphics{lion}	% 目录下的文件名(也可以加入文件后缀名)
	\includegraphics[scale = 0.3,			% 缩放系数
					 height = 2cm,			% 指定高度
					 width = 0.2\textwidth,	% 指定为版型0.2倍的图像宽度
					 angle = -45]			% 旋转角度
\end{document}

% 可使用texdoc graphicx命令查看帮助文档
```

## 八、LaTeX中的表格

```latex
\begin{ducument}
	% 参数分别表示左对齐，居中对齐，右对齐,|用于产生表格竖线,||用于产生双竖线,p用于指定宽度
	\begin{tabular}{|l|c|p{1cm}|c||r}	
		\hline 	% 用于产生表格横线
		第一列	& 第二列 	& 第三列 	& 第四列 	& 第五列 \\ 	% &用于分隔每列,\\用于换行
		\hline	\hline	% 产生双横线
		1 	  & 12		& 89	  & 2		& 0		\\
		\hline
	\end{tabular}
\end{document}

% texdoc booktab 三线表宏包说明文件
% texdoc longtab 长表格宏包说明文件
% texdoc tabu	 综合表宏包说明文件
```

## 九、LaTeX中的浮动体

```latex
\begin{document}
	\LaTeX{}插入图片如图\ref{fig-1}所示		% 交叉引用图片
	\begin{figure}[htbp]	% figure浮动体环境
		\centering	% 环境中的内容居中排版
		\includegraphics[scale=0.3]{pic.jpg}
		\caption{\Tex 插入图片}	% 图片标题及编号
		\label{fig-1}			% 图片标签，以实现交叉引用
	\end{figure}
	
	\LaTeX{}表格见\ref{tab-1}	% 交叉引用表格
	    \begin{table}[h]	% table浮动体环境
            \centering	% 环境中的内容居中排版
            \caption{\LaTeX 插入表格}	% 表格标题及编号
            \label{tab-1}	% 图片标签，以实现交叉引用

            \begin{tabular}{|l|c|p{1cm}|c||r}	
            \hline 	% 用于产生表格横线
            第一列	& 第二列 	& 第三列 	& 第四列 	& 第五列 \\ 	% &用于分隔每列,\\用于换行
            \hline	\hline	% 产生双横线
            1 	  & 12		& 89	  & 2		& 0		\\
            \hline
            
        \end{tabular}
	\end{table}
	
% \beign{figure}[<允许位置>]
% <任意内容>
% \end{figure}

% <允许位置>参数(默认tbp)
% h，此处(here)，即代码所在的上下文位置
% t，页顶(top)，即代码所在页面或之后页面的顶部
% b，页底(buttom)，即代码所在页面或之后页面的底部
% p，单独一页(page)，即浮动页面
```

## 十、LaTeX数学模式

```latex
\section{行内公式}
	$ a+b=b+a $
	\(a+b=b+a\)
	\begin{math}a+b=b+a\end{math}
\section{上标和下标}
	$ x^2 $
	$ x^{20} $
	$ a_1 $
	$ a_{n+1} $
\section{希腊字母}
	$ \alpha $
	$ \beta  $ 
	$ \gamma $ \quad $ \Gamma $
	$ \pi    $ \quad $ \Pi    $
\section{数学函数}
	$ \log $
	$ \sin $
	$ \sqrt{2} $
	$ \sqrt[4]{x} $ % 指定开方次数
\section{分式}
	$ 3/4 $
	$ \frac{3}{4} $
\section{行间公式}
	$$ a+b=b+a $$
	\[a+b=b+a\]
	\begin{displayamth} a+b=b+a \end{displaymath}
\section{自动编号公式}
	交换律公式为\ref{eq-1}
	\begin{equation}
		a+b=b+a	\label{eq-1}
	\end{equation}
	
	% 不带编号:
	交换律公式为\ref{eq-2}	% 此处引用编号为小节编号
	\begin{equation*}		% 需使用amsmath宏包
		a+b=b+a	\label{eq-2}
	\end{equation*}
	
\section{矩阵排版}
	\[	% 环境名称：matrix-无括号,pmatrix-小括号,bmatrix-中括号,Bmatrix-大括号,vmatrix-单竖线,Vmatrix-双竖线
	\begin{matrix}	% 依赖amsmath宏包
        0 & 1 \\
        1 & 0
	\end{matrix}
	\]
	
	\[	
	A = \begin{bmatrix}
	a_{11} 			& \dots  & a_{1n}	\\	% \dots表示横向省略号
	\text{\Large 0}	& \ddots & \vdots	\\	% \ddots表示斜省略号,\text用于在数学模式中临时插入文本
	0      			&        & a_{nn}		% \vdots表示纵向省略号
	\end{bmatrix}_{n_ \times n}		% 矩阵下标
	\]
	
	行内小矩阵使用
	\begin{math}
	\left(	% 手动加上左括号
	\begin{smallmatrix}
	x & -y \\ y & x
	\end{smallmatrix}
	\right)	% 手动加上右括号
	\end{math}来表示
	
\section{多行数学公式}
	\begin{gather}		% 依赖于amsmath包和amssymb包
		a+b=b+a	\\		% 带编号
		a*b=b*a	\notag	% 阻止编号
	\end{gather}		% gather*不带编号
	
	% 按指定位置进行对齐(&用于指定对齐位置)
	\begin{align}		% align*不编号
	x &= t & x &= \cos t & x &=t	\\
	y &= 2t & y &= \sin(t+1) & y &= \sin t
	\end{align}
	
	% 一个公式多行排版
	\begin{equation}
	\begin{split}	% 对齐位置由&指定
	\cos 2x &= \cos^2 x - \sin^2 x	\\
	&= 2\cos^2 x - 1
	\end{split}
	\end{equation}
	
	% cases环境,每行公式中使用&分隔为两部分，用于表示值和值后面的条件
	\begin{equation}
	D(x) = \begin{cases}
	1, & \text{如果}x \in \mathbb{Q};	\\					% mathbb用于输出花体字符
	0, & \text{如果}x \in \mathbb{R}\setminus\mathbb{Q}.
	\end{cases}
	\end{equation}
```

## 十一、LaTeX中的参考文献

### 1、BibTeX

​		首先需要将”选项-构建“中的默认文献工具改为BibTeX。然后创建一个新文件，作为参考文献库，例如：

```latex
@BOOK{mittelbach2004,				% @BOOK指定类型，第一个参数为引用标志
title = {The {{\LaTeX}} Companion},
publisher = {Addison-Wesley},
year = {2004},
author = {Frank Mittelbach and Michel Goossens},
series = {Tools and Techniques for Computer Typesetting},
address = {Boston},
edition = {Second}
}
```

​		保存为.bib文件，采用以下代码调用：

```latex
\bibliographystyle{plain}	% 指定参考文献的排版样式

\begin{document}
	这是一个参考文献的引用：\cite{mittelbach2004}	% 使用\cite引用
	\nocite{*}				% 显示所有未引用的参考文献
	\bibliography{test}		% 指定参考文献数据库，可以不写出后缀，多个库用逗号分隔
\end{document}
```

​		再次编译前清理辅助文件：工具-清理辅助文件。

### 2、BibLaTeX

```latex
\usepackage[style=numeric,backend=biber]{biblatex}	% 导入宏包
\addbibresource{test.bib}	% 导入文献库，不能省略后缀

\begin{document}
	无格式化引用\cite{mittelbach2004}\\
	带方括号的引用\parencite{mittelbach2004}\\
	上标引用\supercite{mittelbach2004}\\
	
	\printbibliography[title={参考文献}]	% 输出参考文献列表
\end{document}
```

## 十二、LaTeX中的自定义命令和环境

### 1、自定义命令

```latex
\newcommand<命令>[<参数个数>][<首参数默认值>]{<具体定义>}

% 简单的字符串替换
\newcommand\RPC{People's Republic of \emph{China}}

% 使用参数
% 参数个数可以从1到9，使用#1表示
\newcommand\loves[2]{#1 喜欢 #2}
\newcommand\love[3][喜欢]{#2#1#3}	% #1参数的默认值为喜欢

% 重定义
\renewcommand\abstractname{内容}	% 只能用于已有的命令
\beign{document}
	\loves{猫}{鱼}
	\love{猫}{鱼}
	\love[最爱]{猫}{鱼}		% 指定第一个参数
	
	\begin{abstract}
		这是一段摘要。
	\end{abstract}
	
\end{document}
```

### 2、自定义环境

```latex
\newenvironment{<环境名称>}[<参数个数>][<首参数默认值>]
			   {<环境前定义>}
			   {<环境后定义>}
% 自定义环境
% 环境参数只有<环境前定义>中可以使用
% <环境后定义>中不能再使用环境参数
% 如果需要，可以先把前面得到的参数保存在一个命令中，在后面是使用
\newenvironment{myabstract[1][摘要]}
{\small	% 设定环境中内容的字号
	\begin{center}\bfseries #1 \end{center}		% 指定#1参数的排版方式
	\begin{quotation}	
}	% 在环境前定义和后定义两端使用大括号
	{\end{quotation}}

% 自定义环境与自定义命令结合
% 解决环境后定义中无法使用参数的问题
\newenvironment{Quotation}[1]
{\newenvironment\quotesource{#1}
	\begin{quotation}}
	{\par\hfill--《\textit{\quotesource}》
	\end{quotation}}

\begin{document}
	\begin{myabstract}[我的摘要]
		这是一段自定义格式的摘要。
	\end{myabstract}
	
	\begin{Quotation}{易$\cdot$乾}
		初九，潜龙勿用。
	\end{Quotation}
\end{document}
```

