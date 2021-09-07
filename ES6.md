## ES6  
ES6를 공부하며 기록합니다  

- [Scope](#scope)  
  - [let](#let)  
- [Array](#array)  
  - [for of](#for-of)  
  - [spread operator(펼침연산자)](#spread-operator펼침연산자)  
  - [from](#from)  
- [Destructuring](#destructuring)
  - [Destructuring Array](#destructuring-array)  
  - [Destructuring Object](#destructuring-object)  


## Scope  

### let

let은 블럭 단위 내에서 접근이 가능하다  

```javascript
function varTest(){
  for(var i = 0; i < 100; i++){}
  console.log(i);
}
varTest();
```
>100  

<br/>

```javascript
function letTest(){
  for(let i = 0; i < 100; i++){}
  console.log(i);
}
letTest();
```
>Uncaught ReferenceError: i is not defined  

var로 생성한 i는 접근이 가능 한 반면, let으로 생성한 i는 for문 블럭 밖에서 접근이 되지 않는 것을 확인할 수 있다  

<br/>

## Array  

### for of  

for of 문으로 배열을 순회할 수 있다  

```javascript
let data = ["cat", 100, undefined, null, "", NaN];
for(let x of data){
  console.log(x);
}
```
>cat  
>100  
>undefined  
>null  
>   
>NaN  

<br/>

배열 뿐만 아니라 문자열도 for of로 순회 가능하다  

```javascript
let str = "A cat!";
for(let s of str){
  console.log(s);
}
```
>A  
>  
>c  
>a  
>t  
>!  

<br/>

### spread operator(펼침연산자)  

spread operator인 ...를 이용해 배열을 펼칠 수 있다  

```javascript
let arr1 = ["cat", 100, undefined, "!", NaN];
let arr2 = [...arr1];
console.log(...arr1);
console.log(arr2);
console.log(arr1 === arr2);
```
>cat 100 undefined ! NaN  
>(5) ["cat", 100, undefined, "!", NaN]  
>false  

[...arr1]는 arr1을 펼친 내용물로 새로운 배열을 만드는 것과 동일하다  
따라서 arr1과 arr2는 서로 다른 객체이다  

<br/>

spread operator는 다음과 같은 활용이 가능하다  

```javascript
let arr1 = ["cold", "and", "sweet"];
let arr2 = ["I", "like", ...arr1, "coffee"];
console.log(arr2);
```
>(6) ["I", "like", "cold", "and", "sweet", "coffee"]  

<br/>

```javascript
function sum(a, b, c){
  return a + b + c;
}
let arr = [1, 2, 3];
console.log(sum(...arr));
```
>6  

<br/>

### from  

Array의 from() 함수로 배열이 아닌 값으로 새로운 배열을 생성할 수 있다  

```javascript
function addMark() {
  let arr = Array.from(arguments);
  let newArr = arr.map(function(value){
    return value + "!";
  });
  console.log(newArr);
}

addMark(1, undefined, 3, "dog", 5, null);
```
>(6) ["1!", "undefined!", "3!", "dog!", "5!", "null!"]  

<br/>

## Destructuring  

### Destructuring Array  

배열에서 필요한 요소한 추출해 변수에 할당할 수 있다  

```javascript
let arr = ["cat", "dog", "parrot", "hamster"];
let [x, , y] = arr;
console.log(x, y);
```
>cat parrot  

<br/>

### Destructuring Object  

객체의 프로퍼티 값을 name으로 추출하고, 새로운 이름의 변수에 할당할 수 있다  

```javascript
let dog = {
  color : "black",
  sound : "bark",
  age : 5
}
let {color, age:old} = dog;
console.log(color);
console.log(old);
```
>black  
>5  

<br/>

