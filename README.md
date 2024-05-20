# ES6-Note
- __const & let__ :
  - 改變變數型態宣告方式，從單純的 var 增加為 定量 const 以及 變量 let。
  - 重複宣告：const 用於宣告常數，不會被重新賦值
  - 作用域不同：
    - var：作用於整個函數範圍中（function scope）
    - let 與 const：均為區塊作用域（block scope），如此可避免污染到大括號外的變數
```CSS
const a = 123;
let b = 123;
a = 456;      // 錯誤a為定量其值不可改變
b = 456;      // b的值已被改變成456
```
- __Template Literals__ :  
  - 改變了以往字串的寫法，不用再用 + 來進行字串與變數的結合。
```CSS
const name = 'Andy';
// ES5寫法
var str = 'Hello' + name + "！";

// ES6寫法
const str = `Hello ${name}！`;
```
  - 也可以多行一起串接
```CSS
// ES5寫法
var html = "<div>";
html +=    "  <p>Hello World</p>";
html +=    "</div>";

// ES6寫法
const html = `
  <div>
    <p>Hello World</p>
  </div>
`
```
- __Destructuring Assignment__
  - 用更簡短的方式宣告陣列或物件的元素的值，不過物件比較麻煩一點，必須要讓變數名稱取名跟 key 一樣的名稱，陣列則不用。
```CSS
  // ES5寫法
  var arr = [1, 2, 3];
  var obj = {d: 1, e: 2, f: 3};
  var a = arr[0],
    b = arr[1],
    c = arr[2];
  var d = obj.d,
    e = obj.e,
    f = obj.f;
  console.log(a, b, c);    // 1 2 3
  console.log(d, e, f);    // 1 2 3

  // ES6寫法
  const arr = [1, 2, 3];
  const obj = {d: 1, e: 2, f: 3};
  const [a, b, c] = arr;   // a = arr[0], b = arr[1], c = arr[2]
  const {d, e, f} = obj;   // d = obj.d, e = obj.e, f = obj.f
  console.log(a, b, c);    // 1 2 3
  console.log(d, e, f);    // 1 2 3
```
- __「反向」的展開：Rest Parameters__
    - 標示所有剩餘的東西(通常跟 Destructuring 搭配使用)
```CSS
function add(…args) { // 會把放進去的值變成一個陣列
 console.log(args);
 return args[0] + args[1]; 
}
console.log(add(1, 2));
// [ 1, 2 ]
// 3
function add(a, ...args) {
 console.log(args);
 return a + args[0]; // 剩餘的變成陣列，所以本來的 b 就變成 args[0]
}
console.log(add(1, 2));
// [ 2 ]
// 3
```
- __Object Literals__
  - 假如 JSON 內的元素其 key 與 value 名稱一樣，可以省略 key 直接寫 value 名稱即可。
```CSS
// ES5寫法
var name = 'Andy';
var obj = {
  name: name
};

// ES6寫法
const name = 'Andy';
const obj = { name };
```
- __Arrow Functions__
  - 讓匿名函式寫法更簡略，寫法為 () => {} ，假如省略大括號的話，代表直接 return 第一行程式碼，假如參數只有一個還可以省略小括號。
```CSS
// ES5寫法
var arr = [1, 2, 3];
var mapArr = arr.map(function(element) {
  return element * 2;
});

// ES6寫法
const arr = [1, 2, 3];
const mapArr = arr.map(element => element * 2);
```
- __Classes__
  - Classes 為新的概念，用於建立物件以及物件繼承上，在使用上必須先 new 一個物件出來才可使用。
```CSS
class square {
  constructor(width, height) {
     this.width = width;
     this.height = height;
  }
  calcArea() {
    return this.width * this.height;
  }
}
const square1 = new square(10, 10);
const area = square1.calcArea();
console.log(area);    // 100
```
