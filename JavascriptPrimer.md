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