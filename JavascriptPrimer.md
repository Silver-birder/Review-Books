＃ 分割代入

[演算子](https://jsprimer.net/basic/operator/)

```javascript
const array = [1, 2];
// aには`array`の0番目の値、bには1番目の値が代入される
const [a, b] = array;
console.log(a); // => 1
console.log(b); // => 2
```

```javascript
const obj = {
    "key": "value"
};
// プロパティ名`key`の値を、変数`key`として定義する
const { key } = obj;
console.log(key); // => "value"
```

[関数と宣言](https://jsprimer.net/basic/function-declaration/)

```javascript
function echo(x = "デフォルト値") {
    return x;
}

console.log(echo(1)); // => 1
console.log(echo()); // => "デフォルト値"
```

Rest parameters (残余引数)

```javascript
function fn(...args) {
    // argsは引数の値が順番に入った配列
    console.log(args); // => ["a", "b", "c"]
}
fn("a", "b", "c");
```

```javascript
const user = {
    id: 42
};
// オブジェクトの分割代入
const { id } = user;
console.log(id); // => 42
// 関数の引数の分割代入
function printUserId({ id }) {
    console.log(id); // => 42
}
printUserId(user);

function print([first, second]) {
    console.log(first); // => 1
    console.log(second); // => 2
}
const array = [1, 2];
print(array);
```

Arrow Functionのthisは、静的に決定する
https://qiita.com/mejileben/items/69e5facdb60781927929

```javascript
param = 'global param';

let printParam = () => {
  console.log(this.param);
}

let object = {
  param: 'object param',
  func: printParam
}
let object2 = {
  param: 'object2 param',
  func: printParam
}

object.func();
object2.func();

// global param
// global param
```

[オブジェクト](https://jsprimer.net/basic/object/)

```javascript
// `version`のプロパティ名が被っている
const objectA = { version: "a" };
const objectB = { version: "b" };
const merged = { 
    ...objectA,
    ...objectB,
    other: "other"
};
// 後ろにある`objectB`のプロパティで上書きされる
console.log(merged); // => { version: "b", other: "other" }
```

```javascript
// 引数の`obj`を浅く複製したオブジェクトを返す
const shallowClone = (obj) => {
    return Object.assign({}, obj);
};
// 引数の`obj`を深く複製したオブジェクトを返す
function deepClone(obj) {
    const newObj = shallowClone(obj);
    // プロパティがオブジェクト型であるなら、再帰的に複製する
    Object.keys(newObj)
        .filter(k => typeof newObj[k] === "object")
        .forEach(k => newObj[k] = deepClone(newObj[k]));
    return newObj;
}
const obj = { 
    level: 1,
    nest: {
        level: 2
    }
};
const cloneObj = deepClone(obj);
// `nest`オブジェクトも再帰的に複製されている
console.log(cloneObj.nest === obj.nest); // => false
```

[プロトタイプオブジェクト](https://jsprimer.net/basic/prototype-object/)

```javascript
// 親がnull、つまり親がいないオブジェクトを作る
const obj = Object.create(null);
// Object.prototypeを継承しないため、hasOwnPropertyが存在しない
console.log(obj.hasOwnProperty); // => undefined
```


```javascript
const map = new Map();
// toStringキーは存在しない
console.log(map.has("toString")); // => false
```

[文字列](https://jsprimer.net/basic/string/)

```javascript
// 呼び出し方によって受け取る引数の形式が変わる
function tag(strings, ...values) {
    // stringsは文字列のパーツが${}で区切られた配列となる
    console.log(strings); // => ["template "," literal ",""]
    // valuesには${}の評価値が順番に入る
    console.log(values); // => [0, 1]
}
// ()をつけずにテンプレートを呼び出す
tag`template ${0} literal ${1}`;
```