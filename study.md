# 第二章 Reactに必要なjavascriptの知識
## 2-1 変数の定義
### 2-1-1 const
const：定数
ES5以前は全ての変数はvarで宣言され、再代入ができた。
```javascript
var pizza = true;
pizza = false;
console.log(pizza); //結果：faise
```
しかしES2015(ES6以降)で導入されたconstを使って再代入しようとすると
```javascript
const pizza = true;
pizza = faise;
console.log(pizza);
```
エラーになる。
> Uncaught TypeError:Assignment to constant variable.

これはconstで再代入できないためにエラーが出る。
再代入する場合はletかvarを使用する。

### 2-1-2 let
letによりjavaScriptにレキシカルスコープが導入された。

レキシカルスコープ（静的スコープ）：

参考元：[wikipedia:静的スコープ](https://ja.wikipedia.org/wiki/%E9%9D%99%E7%9A%84%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%97#:~:text=%E9%9D%99%E7%9A%84%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%97%EF%BC%88%E3%81%9B%E3%81%84%E3%81%A6%E3%81%8D,(lexical%20scope)%20%E3%81%A8%E3%82%82%E3%81%84%E3%81%86%E3%80%82)

例：以下のコードはよくある間違いで、if文がスコープを持たないことを表している。

```javascript
var topic = "JavaScript";
if (topic) {
var topic = "React";
console.log("block", topic); // block React
}
console.log("global", topic); // global React
```
出力結果
```
block React
global React
```
letを使うことでif文のtopic変数はif文の外側から参照できない。
if文と同様にスコープを持たないfor文の場合は
```javascript
var div,
container = document.getElementById("container");
for (var i = 0; i < 5; i++) {
div = document.createElement("div"); //div要素が5つ生成される
div.onclick = function() {
alert("This is box #" + i);
};
container.appendChild(div);
}
```
各div要素をクリックすると「This is box #5」というアラートが生成される。
どのブロックをクリックしても出力結果が全て５になっている。
これは変数iがグローバル変数なので、div要素がクリックされた時のiの値は、グローバル変数iの直近で更新された値である5が表示される。
varを使うと最後の結果、forを抜けた後の5に上書きされる。
[sample3](file:///Users/d.a.kachin/javascript/learning-react-2e-ja-master/chapter-02/2.1/2.1.2/03.html)

次にletを使ってforループ内を書き換えてみる。
```javascript
var div,
container = document.getElementById("container");
for (let i = 0; i < 5; i++) {
div = document.createElement("div");
div.onclick = function() {
alert("This is box #: " + i);
};
container.appendChild(div);
}
```
上記のソースのようにfor文内でletを宣言するとループの繰り返しごとに異なるスコープが生成されるため、

const:定数定義
let：if文内で宣言する
varは使わない