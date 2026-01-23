# 行列と多項式

行列の表記が分かる、また行列の学習時に連立方程式で習った事のある前提で、本来必要な説明をかなり省いています。

## 二元一次方程式と行列表現

行列の計算を習った際に、連立一次方程式が例に挙げられていたと思います。  
これは、多項式の各項の係数を行列に取ることで計算しようというものでした。  

例えば、以下のような二元一次方程式を考え、

```math
\begin{pmatrix}
a_1 & b_1 \\
a_2 & b_2
\end{pmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
=
\begin{bmatrix}
c_1 \\
c_2
\end{bmatrix}
\cdots(1)
```

$x, y$を求めるとき、

```math
A =
\begin{pmatrix}
a_1 & b_1 \\
a_2 & b_2
\end{pmatrix}
```

として、行列では（掃き出し法もありますが）逆行列$A^{-1}$を求めて左から掛け、

```math
A^{-1}A
\begin{bmatrix}
x \\
y
\end{bmatrix} 
=
A^{-1}
\begin{bmatrix}
c_1 \\
c_2
\end{bmatrix}
```

```math
\begin{align*}
E
\begin{bmatrix}
x \\
y
\end{bmatrix} 
&=
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix} 
\begin{bmatrix}
x \\
y
\end{bmatrix} \\
&=
A^{-1}
\begin{bmatrix}
c_1 \\
c_2
\end{bmatrix}
\end{align*}
```

```math
\therefore 
\begin{bmatrix}
x \\
y
\end{bmatrix} 
=
A^{-1}
\begin{bmatrix}
c_1 \\
c_2
\end{bmatrix}
```

より、逆行列$A^{-1}$を求めてから右辺を計算することで解を得たかと思います。

## 連立二次方程式への置き換え

ここで、(1)の式の$x,y$を、それぞれ$x^{2},x$と置き換えると、(1)は、

```math
\begin{pmatrix}
a_1 & b_1 \\
a_2 & b_2
\end{pmatrix}
\begin{bmatrix}
x^2 \\
x
\end{bmatrix}
=
\begin{bmatrix}
c_1 \\
c_2
\end{bmatrix}
\cdots(2)
```

と表現することが出来ます。
通常、二次方程式は$ax^2+bx+c=0$で表現しますが、(2)の左辺を計算すると、

```math
\begin{bmatrix}
a_1x^2 + b_1x \\
a_2x^2 + b_2x
\end{bmatrix}
=
\begin{bmatrix}
c_1 \\
c_2
\end{bmatrix}
```

より、右辺を移項して、

```math
\begin{bmatrix}
a_1x^2 + b_1x - c_1 \\
a_2x^2 + b_2x - c_2
\end{bmatrix}
=
\begin{bmatrix}
0 \\
0
\end{bmatrix}
```

と、（符号はさておき、比較的）見慣れた表現に置き換えられます。  
このように、多項式も「係数を行列として取る」ことで、行列のルールに置き換えて表現・計算することが出来ます。

## 行列上の「微分」

多項式も行列として表現できることが分かったところで、微分の行列表現を大ざっぱに説明します。  
改めて、2次の多項式を係数のベクトルに置き換えることを考えます。  

例えば、

```math
\begin{pmatrix}
a &b &c
\end{pmatrix}
\begin{bmatrix}
x^2 \\ x \\ 1
\end{bmatrix}
```

を計算すると、$ax^2+bx+c$になることが分かります。
このような$[x^2,x,1]^\intercal$（$\intercal$は転置の意味。文中はカンマ付きでこう表現することがあります）とその係数行列で表現される関数$f$を用意し、これを微分するような行列$f'$を考えます。これは、

```math
\begin{align*}
f' &= 
\begin{pmatrix}
0 &2 &1 \\
\quad &0 &0\\
\quad &\quad &0
\end{pmatrix}
\begin{pmatrix}
0 &a &b \\
\quad &0 &0\\
\quad &\quad &0
\end{pmatrix}
\begin{bmatrix}
x^2 \\ x \\ 1
\end{bmatrix}
\\
&= 
\begin{pmatrix}
0 &2a &b \\
\quad &0 &0\\
\quad &\quad &0
\end{pmatrix}
\begin{bmatrix}
x^2 \\ x \\ 1
\end{bmatrix}
\end{align*}
```

と表現出来ないでしょうか。  
この係数行列の第1行のみを解くと、

```math
\begin{align*}
f' &= 0x^2+2ax+b \\
&= 2ax+b
\end{align*}
```

となり、微分を行列として表現出来たと言えないでしょうか。  
生成AIでは、（おそらく）連立高次方程式の係数行列を微分することで計算の省力化を図ろうとしていると考えられます。  
このような方法は、統計の主成分分析でも同じようにベクトルとして置き換えられ、「主成分を求める」ことは「係数行列の微分」を行うことと同じ処理をすると考えられます。

## 行列上の「積分」

行列で微分を（何となく）表現出来たところで、逆の操作である積分を考えてみます。  
二次方程式$f(x)=ax^2+bx+c$について表現すると、

```math
\begin{align*}
f(x)
&=
\begin{pmatrix}
a &b &c \\
\quad &0 &0\\
\quad &\quad &0
\end{pmatrix}
\begin{bmatrix}
x^2 \\ x \\ 1
\end{bmatrix}
\end{align*}
```

とできます。  
ここで、この不定積分$F(x)=\int f(x)dx+C$の形を表現してみます。（$C$は積分定数とし、係数行列内の係数$c$とは異なります）

```math
\begin{align*}
F(x)
&=
\begin{pmatrix}
\frac{1}{3} &\frac{1}{2} &1 &0 \\
\quad &0 &0 &0 \\
\vdots &\quad &0 &0 \\
0 &\cdots &\quad &0
\end{pmatrix}
\begin{pmatrix}
a &b &c &0 \\
\quad &0 &0 &0 \\
\vdots &\quad &0 &0 \\
0 &\cdots &\quad &0
\end{pmatrix}
\begin{bmatrix}
x^3 \\ x^2 \\ x \\ 1
\end{bmatrix}
+
\begin{bmatrix}
0 \\ 0 \\ 0 \\ C
\end{bmatrix}
\\
&=
\begin{pmatrix}
\frac{1}{3}a &\frac{1}{2}b &c &0 \\
\quad &0 &0 &0 \\
\vdots &\quad &0 &0 \\
0 &\cdots &\quad &0
\end{pmatrix}
\begin{bmatrix}
x^3 \\ x^2 \\ x \\ 1
\end{bmatrix}
+
\begin{bmatrix}
0 \\ 0 \\ 0 \\ C
\end{bmatrix}
\\
&=
\begin{bmatrix}
\frac{1}{3}ax^3+\frac{1}{2}bx^2+cx+C
\end{bmatrix}^\intercal
\end{align*}
```

以上より、積分も行列で表現出来るといえます。  
これらの発展から、三次以上の高次方程式も、多変数の多項式も同様に、係数を割り当てることで表現出来るといえます。  

実際には手順は異なりますが、「微分積分、あるいは人工知能分野での行列計算で表現されているものはおおよそこうである」という理解は可能だと思います。

## 理解の助けにおすすめの理数書

- [中学数学＋α でわかる線形代数のエッセンス（技術評論社）](https://gihyo.jp/book/2024/978-4-297-14540-8)
  - 行列の意味合いを何となく知っておくと、次の「半歩先」の繋ぎとして良いと思います。
- [線形代数の半歩先 データサイエンス・機械学習に挑む前の30話(講談社サイエンティフィク)](https://www.kspub.co.jp/book/detail/5386477.html)
  - 大学基礎数学の線形代数学の講義を受けたことのある（受けている）人向け。「基礎」と「応用」の繋ぎとして良いと思います。

(以上)
