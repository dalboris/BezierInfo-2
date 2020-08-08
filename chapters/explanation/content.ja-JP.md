# ベジエ曲線の数学

ベジエ曲線は「パラメトリック」関数の一種です。数学的に言えば、パラメトリック関数というのはインチキです。というのも、「関数」はきっちり定義された用語であり、いくつかの入力を<strong>1つ</strong>の出力に対応させる写像を表すものだからです。いくつかの数値を入れると、1つの数値が出てきます。入れる数値が変わっても、出てくる数値はやはり1つだけです。パラメトリック関数はインチキです。基本的には「じゃあわかった、値を複数個出したいから、関数を複数個使うことにするよ」ということです。例として、ある値<i>x</i>に何らかの操作を行い、別の値へと写す関数があるとします。

\[
  f(x) = \cos(x)
\]

<i>f(x)</i>という記法は、これが関数（1つしかない場合は慣習的に<i>f</i>と呼びます）であり、その出力が1つの変数（この場合は<i>x</i>です）に応じて変化する、ということを示す標準的な方法です。<i>x</i>を変化させると、<i>f(x)</i>の出力が変化します。

ここまでは順調です。では、パラメトリック関数について、これがどうインチキなのかを見てみましょう。以下の2つの関数を考えます。

\[
\begin{matrix}
  f(a) = \cos(a) \\
  f(b) = \sin(b)
\end{matrix}
\]

注目すべき箇所は特に何もありません。ただの正弦関数と余弦関数です。ただし、入力が別々の名前になっていることに気づくでしょう。仮に<i>a</i>の値を変えたとしても、<i>f(b)</i>の出力の値は変わらないはずです。なぜなら、こちらの関数には<i>a</i>は使われていないからです。パラメトリック関数は、これを変えてしまうのでインチキなのです。パラメトリック関数においては、どの関数も変数を共有しています。例えば、

\[
\left \{ \begin{matrix}
  f_a(t) = \cos(t) \\
  f_b(t) = \sin(t)
\end{matrix} \right.
\]

複数の関数がありますが、変数は1つだけです。<i>t</i>の値を変えた場合、<i>f<sub>a</sub>(t)</i>と<i>f<sub>b</sub>(t)</i>の両方の出力が変わります。これがどのように役に立つのか、疑問に思うかもしれません。しかし、実際には答えは至ってシンプルです。<i>f<sub>a</sub>(t)</i>と<i>f<sub>b</sub>(t)</i>のラベルを、パラメトリック曲線の表示によく使われているもので置き換えてやれば、ぐっとはっきりするかと思います。

\[
\left \{ \begin{matrix}
  x = \cos(t) \\
  y = \sin(t)
\end{matrix} \right.
\]

きました。<i>x</i>/<i>y</i>座標です。謎の値<i>t</i>を通して繫がっています。

というわけで、普通の関数では<i>y</i>座標を<i>x</i>座標によって定義しますが、パラメトリック曲線ではそうではなく、座標の値を「制御」変数と結びつけます。<i>t</i>の値を変化させるたびに<strong>2つ</strong>の値が変化するので、これをグラフ上の座標 (<i>x</i>,<i>y</i>)として使うことができます。例えば、先ほどの関数の組は円周上の点を生成します。負の無限大から正の無限大へと<i>t</i>を動かすと、得られる座標(<i>x</i>,<i>y</i>)は常に中心(0,0)・半径1の円の上に乗ります。<i>t</i>を0から5まで変化させてプロットした場合は、このようになります（上下キーでプロットの上限を変更できます）。

<Graphic title="（部分）円 x=sin(t), y=cos(t)" static={true} setup={this.setup} draw={this.draw} onKeyDown={this.props.onKeyDown}/>

ベジエ曲線はパラメトリック関数の一種であり、どの次元に対しても同じ基底関数を使うという点で特徴づけられます。先ほどの例では、<i>x</i>の値と<i>y</i>の値とで異なる関数（正弦関数と余弦関数）を使っていましたが、ベジエ曲線では<i>x</i>と<i>y</i>の両方で「二項係数多項式」を使います。では、二項係数多項式とは何でしょう？

高校で習った、こんな形の多項式を思い出すかもしれません。

\[
  f(x) = a \cdot x^3 + b \cdot x^2 + c \cdot x + d
\]

最高次の項が<i>x³</i>であれば3次多項式、<i>x²</i>であれば2次多項式と呼び、<i>x</i>だけの場合は1次多項式――ただの直線です。（そして<i>x</i>の入った項が何もなければ、多項式ではありません！）

ベジエ曲線は<i>x</i>の多項式ではなく、<i>t</i>の多項式です。<i>t</i>の値は0から1までの間に制限され、その係数<i>a</i>、<i>b</i>などは「二項係数」の形をとります。というと複雑そうに聞こえますが、実際には値を組み合わせて、とてもシンプルに記述できます。

\[
\begin{aligned}
  1次 &= (1-t) + t \\
  2次 &= (1-t)^2 + 2 \cdot (1-t) \cdot t + t^2 \\
  3次 &= (1-t)^3 + 3 \cdot (1-t)^2 \cdot t + 3 \cdot (1-t) \cdot t^2 + t^3
\end{aligned}
\]

「そこまでシンプルには見えないよ」と思っていることでしょう。しかし仮に、<i>t</i>を取り去って係数に1を掛けることにしてしまえば、急激に簡単になります。これが二項係数部分の項です。

\[
\begin{aligned}
  1次 &= \hspace{2.5em} 1 + 1 \\
  2次 &= \hspace{1.7em} 1 + 2 + 1\\
  3次 &= \hspace{0.85em} 1 + 3 + 3 + 1\\
  4次 &= 1 + 4 + 6 + 4 + 1
\end{aligned}
\]

2は1+1に等しく、3は2+1や1+2に等しく、6は3+3に等しく、……ということに注目してください。見てわかるように、先頭と末尾は単に1になっていますが、中間はどれも次数が増えるたびに「上の2つの数を足し合わせた」ものになっています。<i>これなら</i>覚えやいですね。

多項式部分の項がどうなっているのか、同じぐらい簡単な方法で考えることができます。仮に、<i>(1-t)</i>を<i>a</i>に、<i>t</i>を<i>b</i>に書き換え、さらに重みを一旦削除してしまえば、このようになります。

\[
\begin{aligned}
  1次 &= BLUE[a] + RED[b] \\
  2次 &= BLUE[a] \cdot BLUE[a] + BLUE[a] \cdot RED[b] + RED[b] \cdot RED[b] \\
  3次 &= BLUE[a] \cdot BLUE[a] \cdot BLUE[a] + BLUE[a] \cdot BLUE[a] \cdot RED[b] + BLUE[a] \cdot RED[b] \cdot RED[b] + RED[b] \cdot RED[b] \cdot RED[b]\\
\end{aligned}
\]

これは要するに、「<i>a</i>と<i>b</i>のすべての組み合わせ」の単なる和です。プラスが出てくるたびに、<i>a</i>を<i>b</i>へと1つずつ置き換えていけばよいのです。こちらも本当に単純です。さて、これで「二項係数多項式」がわかりました。完璧を期するため、この関数の一般の形を示しておきます。

\[
  Bézier(n,t) = \sum_{i=0}^{n}
                \underset{二項係数部分の項}{\underbrace{\binom{n}{i}}}
                \cdot\
                \underset{多項式部分の項}{\underbrace{(1-t)^{n-i} \cdot t^{i}}}
\]

そして、これがベジエ曲線の完全な表現です。この関数中のΣは、加算の繰り返し（Σの下にある変数を使って、...=<値>から始めてΣの下にある値まで）を表します。

<div className="howtocode">

### 基底関数の実装方法

上で説明した関数を使えば、数学的な組み立て方で、基底関数をナイーブに実装することもできます。

```
function Bezier(n,t):
  sum = 0
  for(k=0; k<n; k++):
    sum += n!/(k!*(n-k)!) * (1-t)^(n-k) * t^(k)
  return sum
```

「こともできる」と書いたのは、この方法では実装しない方が良いからです。階乗は*とてつもなく*重い計算なのです。また、先ほどの説明からわかるように、実際は階乗を使わなくても、かなり簡単にパスカルの三角形を作ることができます。[1]から始めて[1,1]、[1,2,1]、[1,3,3,1]、……としていくだけです。下の段は上の段よりも1つ要素が増え、各段の先頭と末尾は1になります。中間の数はどれも、左右斜め上にある両要素の和になります。

このパスカルの三角形は、「リストのリスト」として瞬時に生成できます。そして、これをルックアップテーブルとして利用すれば、二項係数を計算する必要はまったくなくなります。

```
lut = [      [1],           // n=0
            [1,1],          // n=1
           [1,2,1],         // n=2
          [1,3,3,1],        // n=3
         [1,4,6,4,1],       // n=4
        [1,5,10,10,5,1],    // n=5
       [1,6,15,20,15,6,1]]  // n=6

binomial(n,k):
  while(n >= lut.length):
    s = lut.length
    nextRow = new array(size=s+1)
    nextRow[0] = 1
    for(i=1, prev=s-1; i<s; i++):
      nextRow[i] = lut[prev][i-1] + lut[prev][i]
    nextRow[s] = 1
    lut.add(nextRow)
  return lut[n][k]
```

これはどのように動くのでしょう？最初に、十分に大きなサイズのルックアップテーブルを宣言します。次に、求めたい値を得るための関数を定義します。この関数は、求めたい値のn/kのペアがテーブル中にまだ存在しない場合、先にテーブルを拡張するようになっています。さて、これで基底関数は次のようになりました。

```
function Bezier(n,t):
  sum = 0
  for(k=0; k<=n; k++):
    sum += binomial(n,k) * (1-t)^(n-k) * t^(k)
  return sum
```

完璧です。もちろん、さらなる最適化を施すこともできます。コンピュータグラフィクス用途ではたいてい、任意の次数の曲線が必要になるわけではありません。2次と3次の曲線だけが必要であれば、以下のようにコードを劇的に単純化することができます（実際、この入門では任意の次数までは扱いませんので、これに似たようなコードが出てきます）。

```
function Bezier(2,t):
  t2 = t * t
  mt = 1-t
  mt2 = mt * mt
  return mt2 + 2*mt*t + t2

function Bezier(3,t):
  t2 = t * t
  t3 = t2 * t
  mt = 1-t
  mt2 = mt * mt
  mt3 = mt2 * mt
  return mt3 + 3*mt2*t + 3*mt*t2 + t3
```

これで基底関数をプログラムする方法がわかりました。すばらしい。

</div>

というわけで、基底関数がどのようなものか理解できました。今度はベジエ曲線を特別にする魔法――制御点を導入する時間です。