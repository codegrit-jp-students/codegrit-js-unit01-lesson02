## オブジェクト型

### オブジェクト(Object)

プリミティブ型が不変であるのに対して、オブジェクト型は可変であるということを、このレッスンの冒頭でも述べました。

オブジェクトはいわゆる入れ物=箱のようなものであり、時間とともに中に入る内容物も変わって来ます。
入れ物としての箱は変わらず、箱の中身だけが時間や処理の進行に伴って変わっているイメージです。

その入れ物の中身の内容として、複数の値や複雑な値を入れておくことができるのです。

箱の中身がわかりやすいように、入れ物には中身の内容がわかるような名前をつけておくのが基本です。

オブジェクトがどんな役割をするのか、何となくイメージができたところで、実際にオブジェクトを使ってみましょう。
まずオブジェクトの書き方と構成について、簡単に記憶してから書いていきましょう。

入れ物の箱であるオブジェクトに記憶される内容物のことを**_プロパティ（property）_**と呼びます。
CSSにも出て来たので、CSSのプロパティとJavaScriptのプロパティを混同しないように気をつけましょう。
JavaScriptのプロパティは**名前(key)**と**値(value)**から成り立ち、プロパティの名前のことを**キー**と呼ぶこともあります。

キーとして使用できるのは文字列と、レッスン7で詳しく学ぶ方の1つ**_シンボル_**です。

試しに簡単に空のオブジェクトを作成して、プロパティに`color`を追加してみます。

```js
const obj = {};
obj.color = 'yellow';
console.log(obj.color);// yellowがアウトプットとして表示される
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/mjr1o5p9/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

上記では`obj.color`というプロパティにアクセスするためのドット「.」を含める、**_メンバーアクセス演算子_**という方法を用いました。
この方法を用いることにより、プロパティ、つまり入れ物の箱であるオブジェクトの中身が何であるかを知ることができるのです。

実は、上記の方法は`obj.['color']`に書き換えても結果は同じになります。
どういうことかというと、「[]」（ブラケットと言います）で囲まれた部分を文字列で認識されます。
つまり、プロパティ名がスペースのように有効ではない名前であっても良いように文字列として認識するための方法です。
これを**計算値によるメンバーアクセス(computed member access)**と呼びます。

`color`のような有効な識別子のプロパティは、有効とみなされない識別子としての書き方でも、通常のメンバーアクセスの書き方でも認識されるというわけです。

ここまで空のオブジェクトを作ってみましたが、オブジェクトはプロパティの値を指定して生成することもできます。
簡単に構成を表記すると以下のようになります。

```js
const obj = {
  名前(文字列の場合はキー): '値',
  name: 'value',
};
```

上記の構成はオブジェクトのリテラル構文です。
上記の構成を覚えておいて、まず2つのオブジェクトを試しに生成してみます。

```js
const obj1 = {
  name: 'Lisa',
  nationality: 'Japanese',
};
console.log(obj1); // アウトプットは {name: "Lisa", nationality: "Japanese"}
console.log(obj1.name); // Lisaがアウトプットされる
console.log(obj1.nationality); // Japaneseがアウトプットされる

const obj2 = { name: 'Lisa', nationality: 'Japanese' }; // 1行で宣言 & 内容（プロパティ）はobj1と同じ
console.log(obj2); // アウトプットも同じ
console.log(obj1.name);
console.log(obj1.nationality);
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/dxshyvqp/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

`obj1` と `obj2` はオブジェクトに穀される内容、つまりプロパティが同じでも、オブジェクトとしては全く別のものとして認識されることに注意しましょう。その証拠が以下の検証結果です。

```js
console.log(obj1.name === obj2.name); // true
console.log(obj1.nationality === obj2.nationality); // true
console.log(obj1 === obj2); // false
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/g1Lfpkj0/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

プロパティである、`name`と`nationality`は`obj1`も`obj2`も同じプロパティですが、`obj1`と`obj2`は異なるオブジェクトなので、詳しくはレッスン3の演算子の内容で学びますが、 `===` は、同じオブジェクであるか、プリミティブ型で、データ型も値も同じであるかどうかの全てが厳密に比較されるので、異なるオブジェクトのobj1とobj2は`obj1 === obj2`で`false`となった訳です。

オブジェクトの他の特徴の1つとして、オブジェクトは関数を持つことができ、以下のように使用することができます。
※　オブジェクトのプロパティとして使われる関数は、**_メソッド_**と言います。

```js
obj1.name = function() { return 'I\'m Lisa.' };
obj2.name = function() { return 'I\'m also Lisa, but a different one.' };

// 関数を呼び出すには、プロパティに()をつけて以下のように呼び出す。
console.log(obj1.name()); // I'm Lisa.
console.log(obj2.name()); // I'm also Lisa but a different one.
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/ec049L5x/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

### 配列(Array)

配列（Array）は、オブジェクトと非常によく似ていおり、オブジェクトのように複数のデータを一度に処理するために存在する構造です。
詳しくはレッスン10で学びますが、ここでも少し概要を学んでおきましょう。

配列がオブジェクトと異なる点は、特別なタイプのオブジェクトとして扱われるため、配列に記憶されるデータには順番が決まっていて、キー（プロパティの名前）は0から始まる一連の整数です。
書き方も少し異なり、`[1, 2, 3, 4]`と、以下のように、配列要素を「[]」ブラケットで囲んで書きます。

```js
const arraySample = [1, 2, 3];
const randomType = [
  4,
  true,
  6,
  'seven',
  'ランダムな型も配列に含めることができます'
];
```

ランダムに異なる型も配列要素に含めることができるので、オブジェクトを配列要素にすることも、配列自体を配列要素にすることもできてしまいます。

```js
const objArray = [
  { name: 'Alex', age: 28 },
  { name: 'Samuel', age: 15 },
];

const arrayArray = [
  [0, 1, 2],
  [3, 4, 5, 6],
];
```

配列内に合計でいくつ要素があるかということも`length`を使用して返すことができます。
ただし、特定の要素にアクセスしたいときは、0から数える必要があるので、1番目の要素にアクセスしたい場合は以下のように書きます。

```js
const arraySample = [1, 2, 3];
console.log(arraySample.length); // 3
console.log(arraySample[0]); // 1

const objArray = [
  { name: 'Alex', age: 28 },
  { name: 'Samuel', age: 15 },
];
console.log(objArray[0].name); // Alex
console.log(objArray[1].age); // 15
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/9fr5xh0d/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

特定要素にアクセスできることを利用して、以下のように特定の配列要素を書き換えることもできます。

```js
const swapArray = [
  'axela sedan',
  'Mazda',
  'pixis mega',
  'Toyota'
];

swapArray[0] = 'BMW';
swapArray[2] = 'Mercedes-Benz';
console.log(swapArray); // ['BMW', 'Mazda', 'Mercedes-Benz', 'Toyota']
console.log(swapArray.length); // 4
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/L0oakph6/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

> ※　注意！
>
> 配列やオブジェクトの最終要素の後ろについている「,」は、データ交換で使用されるJSONでは禁止されていますが、配列やオブジェクトはInternet Explorerの古いバージョンを除いて「,」はエラーにならないのでつけても構いません。

### 日時(Date)

よく使用する日時の組み込みオブジェクトに`new Date()`があり、現在の日時を生成することができます。
実用面でまだまだ使い勝手が良いとは言えませんが、オブジェクトのプロパティとして使われる関数（メソッド）を使用すると私たちが普段馴染みのある年、月、日、時間をそれぞれに分けて取得することが可能です。

メソッドを使用しない場合と使用した場合とを見比べてみましょう。

```js
const now = new Date();
console.log(now); // Mon Apr 09 2018 23:55:53 GMT+0200 (CEST)

// ただしアウトプットは処理系によって異なる
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/1as3rk6c/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

上記はメソッドを使用しない例です。
それなりに整っているように上記では見えますが、これは処理系によるため、中には`2018-04-09T07:52:50.564Z`のようなアウトプット(これをISO表記と呼びます。)を返すものもあります。
上記に比べると処理系が異なるだけでこんなに表示の仕方が変わるので、特に見辛い表記が返される処理系の場合は困りますよね。

今度はメソッドを使用してみましょう。
```js
const now = new Date();

console.log(now.getFullYear()); // 2018
console.log(now.getMonth()); // 月は0からカウントされるため4月であれば「3」
console.log(now.getDate()); // 日も同様
console.log(now.getDay()); // 曜日も0（日曜日）、1（月曜日）...となる
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/9corx5n2/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

この他にも`getHours()`、`getMinutes()`、`getSeconds()`、`getMilliseconds()`といったメソッドがあります。
`2018-04-09T07:52:50.564Z`のような表記よりは、0から曜日や月をカウントするとは言え、配列の特定要素へのアクセスと共通することなので、まだ私たちが普段馴染みある表記に近いアウトプットを返してくれます。

`new Date()`は使い勝手が良いとは言えないところもあり、実用的かと言われれば、難しいところがあります。そのため、**Moment.js**のようなライブラリを使用するのが、最近では主流です。

## 更に学ぼう

### 動画で学ぶ

- [JavaScript入門 - ドットインストール](https://dotinstall.com/lessons/basic_javascript_v2)

### 本で学ぶ

- [Eloquent JavaScript 3rd Edition](http://eloquentjavascript.net/)
