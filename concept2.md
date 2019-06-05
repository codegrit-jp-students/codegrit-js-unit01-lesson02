## プリミティブ型

### 数値(Number)

JavaScriptでは、もちろん計算もできます。
ただし全ての数字に関して計算が電卓で行ったように結果が出るかというと、実は「あること」が関係しているため、そうもいかないことがあります。

試しに以下の内容をGoogle developer tool を開いて、Consoleタブで計算してみましょう。

```js
const a = 0.1 + 0.2;
console.log(a);
```

単純に 0.1 + 0.2 の答えは電卓や暗算で行うと、もちろん 0.3 になるはずです。
ところが、JavaScriptの計算結果では以下のようになります。

```
0.30000000000000004
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/pg1y4w3n/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

なぜでしょうか？
実はJavaScriptで適用される数値の表現は、**IEEE 754-2008**という**倍精度浮動小数点数（64ビット）**の表現を使用するために、計算結果が上記のようになるケースもあります。

もっと具体的に解説していきます。
数値の中にはコンピューターで表現できるものとできないもの（πなど）があるため、表現できないものは**近似値**で表現されます。
近似値で表現された数値の計算なので、組み合わせによって計算ミスのような結果が出る場合もあるのです。

別の例でいうと、πなどの無限にある桁数の数値と、限りのある有限の数値を計算することはできないので、コンピューターで表現できる近似値に無限にある数値を当てはめるため、こうしたことが起こります。

```
※  さらに踏み込むとJavaScriptは、他の言語と少し異なる点があり、整数と浮動小数点数を区別せず、全ての数値を浮動小数点数で表します。
```

そのため、JavaScriptは電卓アプリなど、整数演算や固定小数点数の精度が求められるアプリの開発には不向きだということがわかります。

特殊な例として、以下のような値も結果として返ってくる場合があります。

```js
console.log(1/0);// 計算結果 --> Infinity (無限大)
console.log(-1/0);// 計算結果 --> -Infinity（負の無限大）
console.log(Infinity/Infinity);// 計算結果 --> NaN（Not a numberの略）
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/tx06g1d7/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

計算結果が思っていたものと違った場合、上記のように0で数値を割ってしまっている可能性を疑いましょう。

### 文字列(Strings)

文字列（Strings）は、英訳通り文字の連続した列です。
文字列をリテラル、つまりテキスト文字として表示させるには「" " ダブルクォート」か、「' ' シングルクォート」で囲みます。
基本的には、シングルクォートとダブルクォートどちらも使っていいですが、スタイルガイドとして、基本全てシングルクォートを使うのが良いとされています。

例えば「Hello, world!」の文章を文字列リテラルとして表示させるには以下のように文字列を囲むことで、文字列リテラルとして表示させることができます。

```js
const phrase = 'Hello, world!';
console.log(phrase); // Hello, world! がアウトプットされる
```

しかし、引用符の「" "」や「' '」自体が文字列中に含まれている場合はどうなるのでしょうか？

この場合、ダブルクォートで囲った文字列の中にシングルクォートを使ったり、シングルクォートで囲った文字列にダブルクォートを利用するのは問題ありません。

```js
const longPhrase = 'When I say "Hello, world!" in this way, it works.';
console.log(longPhrase); // When I say "Hello, world!" in this way, it works.がアウトプットされる

const sentence = "Even if I say 'Hello, world!' like this way, it also works.";
console.log(sentence); // Even if I say 'Hello, world!' like this way, it also works.がアウトプットされる
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/k8wfadem/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

しかし、ダブルクォートで囲った文の中にダブルクォートを入れてしまうとそこで一旦文字列が終わってしまいエラーが発生します。こうした時には、`バックスラッシュ(\)`を利用することで、ここで文字列は終わらないよ、とブラウザに教えてあげる必要があります。

バックスラッシュはMacの場合は、**option + ¥**で入力出来ます。

```js
const escapeEx = 'I\'m a computer engineer.';
console.log(escapeEx);
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/8w7zt6a5/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

また、ES6では**バッククォート`**を利用して変数を埋め込んだ文字列を作成できるようになりました。バッククォートを用いた書き方のことを**_テンプレートリテラル_**と呼びます。

例えば以下の例を見てみましょう。

```js
let currentRole = 'student';
const phrase = `I'm a ${currentRole}.`;

console.log(phrase); // I'm a student.がアプトプットされる
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/nf9rm3kp/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

上記の例では、`currentRole`という変数を文字列に埋め込んでいます。

上記と同一の内容を`'I\'m a ' + currentStatus`と書くことも出来ますが、テンプレートリテラルがより可読性が高いため、文字列と文字列を含む変数を結合したい場合、テンプレートリテラルを使うのが推奨です。

また文字列全てにテンプレートリテラルを使うのではなく、通常はシングルクォート「''」を使い、変数がある場合のみテンプレートリテラルを使いましょう。

ところで、数字を文字列で表示させたい場合はどうしたら良いのでしょうか？

答えは非常に簡単で、シングルクォートやダブルクォートで囲まれた数字は文字列として認識されます。（※  厳密に言うと、認識される場合とされない場合とに分かれますが、データ型の変換と言う内容で詳細は学びます。）

### 論理値（真偽値、Boolean）

論理値は`true`もしくは`false`どちらかの値を取ります。英訳の通り、「真」か「偽」です。

JavaScriptでは数値以外も含めた全ての値を`true`か`false`として扱っています。
書き方に少し注意が必要で、`"false"`のようにダブルクォートで囲んでしまうと文字列として認識され、falseであっても`true`として処理されてしまうので、以下のように書きましょう。

```js
let shin = true;
let gi = false;
```

### null、undefined

`null`と`undefined`は、どちらも「存在しないもの」を表す「表現」です。
「存在しないもの」であれば表現できないのでは？と、思われたかもしれません。
ではなぜ「存在しないもの」を表現する必要があるのでしょうか？

答えは、JavaScriptの処理系のためには、存在しないものであっても表現する必要があるからです。

まだピンとこない答えかもしれませんが、要するに、何かしらの値として利用できるのが`null`です。

それに対し、`undefined`は値をまだ指定される前の状態の表現です。

開発者が変数などの値として利用したい時に使うことができる`データ型`としてであれば`null`が使えますが、`undefined`は値がそもそもまだ指定されていないことを表しているので、データ型としては使えないのです。

### シンボル

シンボル型はES6で新しく追加された型です。応用コースのレッスン7で学ぶためここでは触れません。