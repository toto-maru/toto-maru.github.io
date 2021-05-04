---
layout: post
title:  "代数的データ型に入門する"
date:   2021-05-03 16:17:59 +0900
categories: CategoryTheory
---
## 代数的データ型とは
代数的データ型とは、代数が成り立つデータ型のこと。
入門するときにまず出てくるのが、Sum type (足し算に相当するデータ型)と、Product type (掛け算に相当するデータ型)の２つ。

Sum typeとProduct typeには関係があって、ProductとCo-Productの関係。

Productを考えると、Co-Productの関係は、圏論ではDualityと言う。どちらか一方を見つけると、その反対(すべてのarrowを反転させた圏)も圏としての性質を満たす。

### Sum typeの性質を持つデータ型
#### タプル（組）
一般的には異なるデータ型を一つにまとめたデータ型。
ほとんどの言語で、言語自体が提供している。

例えばPythonなら
{% highlight python %}
a = (1, "hello") # (int, string)

def isOverN(n, user):
    age, _ = user
    return age > n
isOver18 = lambda user: isOverN(18, user)
isOver18(a) # False
{% endhighlight %}

Haskellなら
{% highlight haskell %}
data User = User Int Int String
isOverN:: Int -> User -> Bool
isOverN t (User age _) = age > t

isOver18 = isOverN 18
isOver18 (User 7 "totomaru") -- False
isOver18 (User 20 "young adult") -- True
{% endhighlight %}

ここまで見るてもタプルの「代数的」な性質については説明していない。
「代数的」といっているのは、「代数（四則演算）」のようなものがデータ型自体に成り立つから代数的といっている（実際は引き算や割り算に相当する概念は成立しないなど、限定的な代数）。
{% highlight python %}
a = (1, 2, 3)
b = (4, 5)
# 通常の足し算が成り立つ
a + b # => (1, 2, 3, 4, 5)
# a + 0 = a
zero = ()
a_zero_added = a + zero
a == a_zero_added # True => 同じ要素が同じ順番に並んでいる
{% endhighlight %}
一方でHaskellでは言語の標準機能としてはタプルの結合操作を提供しないので、言語標準のタプル型は上記のPythonのようになことはすぐにはできない。

タプルではなく、リストならHaskellの標準機能として結合操作が提供される。ということでリストを見てみよう。

#### リスト
一般的には同じデータ型を複数並べたものを一つにまとめたデータ型。
タプルと同じくほとんどの言語で、言語自体が提供するデータ型だが、要素数が動的に変更できる場合(PythonやHaskellのリスト)とそうで無い場合(例えばRustのarray)がある。


## monoid
- 要素の集合
- 二項演算子（2つの要素を取る演算）
- ユニット要素（要素の集合から任意の一つの要素を選んで、その要素とユニット要素に二項演算子を適応しても、もとの任意の要素が変化しないもの）
からなる圏をmonoidという。

たとえば、
- 自然数の集合
- 「+」の二項演算
- ユニット要素「0」
とするとこの圏（圏は絵を書いたほうがわかりやすい）はmonoidだ。
他にも、

中身は違えど、「monoid」とうい共通の性質を持っているので、「monoidであるという点で同じ」といるレベルまで抽象化してしまえば、「同じもの」と捉えることができる。
「ここまで抽象化したレベルでは同じものと捉えられる」という考え方は圏論ではよく出てくる。

### リスト


