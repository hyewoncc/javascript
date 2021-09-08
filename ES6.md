## ES6  
ES6를 공부하며 새로 배운 사실을 기록합니다  

- [Scope](#scope)  
  - [let](#let)  
- [Array](#array)  
  - [for of](#for-of)  
  - [spread operator(펼침연산자)](#spread-operator펼침연산자)  
  - [from](#from)  
- [Destructuring](#destructuring)
  - [Destructuring Array](#destructuring-array)  
  - [Destructuring Object](#destructuring-object)  
- [Set](#set)  
  - [WeakSet](#weakset)  
- [Template](#template)  
  - [Template](#template-1)  
  - [Tagged Template Literals](#tagged-template-literals)  
- [function](#function)  
  - [Arrow function의 this context](#arrow-function의-this-context)  
  - [default parameters](#default-parameters)  
  - [rest parameters](#rest-parameters)


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

## Set

### WeakSet  

weakset은 참조를 가지고 있는 객체만 저장이 가능하다  
배열, 함수 등의 객체가 여기에 해당하며,  
기본 타입인 숫자, 문자열, boolean, null, undefined는 저장 불가능하다  
이는 해당 객체가 null이 되거나 필요가 없어지면 가비지 컬렉션 대상이 되어 weakset에서도 없어지게 된다는 의미다  

```javascript
let ws = new WeakSet();
let x = [1, 2, 3, 4];
let y = [5, 6, 7, 8];
let z = {x, y};

ws.add(x).add(y).add(z);
console.log(ws);

x = null;
console.log(ws);

console.log(ws.has(x), ws.has(y));
```
>WeakSet {Array(4), Array(4), {…}}  
>WeakSet {Array(4), Array(4), {…}}  
>false true  

처음 x, y, z를 추가한 후 콘솔에 출력하면 당연히 해당 객체들이 들어있다고 나온다  
이후 x를 null로 설정 후 콘솔에 출력하면 여전히 x가 들어있는 것 처럼 나오지만,  
has 메소드로 확인 시 x는 false로 들어있지 않고, y는 true로 들어있다는 결과를 보여준다  
이는 null로 설정 된 x가 가비지 콜렉션 대상이며 weakset에서 없어진 게 맞다는 것이다  

<br/>

## Template  

### Template  

json 데이터를 다룰 때 백틱(`)을 이용해 다음과 같은 방식으로 DOM을 조작할 수 있다  

```javascript
const data = [
  {
    animal : 'cat',
    color : 'gray', 
    foods : ['fish', 'tuna', 'snack']
  },
  {
    animal : 'dog', 
    color : 'black', 
    foods : ['jerky', 'meet']
  }
]

const template = `<div>I gave my ${data[0].color} ${data[0].animal} a ${data[0].foods[2]}</div>`
                + `<div>You gave your ${data[1].color} ${data[1].animal} a ${data[1].foods[0]}</div>`;
console.log(template);
```
>`<div>I gave my gray cat a snack</div><div>You gave your black dog a jerky</div>`   

<br/>

### Tagged Template Literals  

데이터마다 갖고 있는 정보 양식에 차이가 있을 때, 다음과 같이 Tagged Template Literals 함수를 만들어  
데이터를 파싱한 후 넘겨줄 수 있다  

```javascript
const data = [
  {
    animal : 'cat',
    color : 'gray', 
    foods : ['fish', 'tuna', 'snack']
  },
  {
    animal : 'dog', 
    color : 'black', 
  }
]

function feed(tags, color, animal, foods) {
  if(typeof foods === "undefined"){
    foods = "nothing";
  }
  return (tags[0] + color + tags[1] + animal + tags[2] + foods + tags[3]);
}
data.forEach((d) => {
  let template = feed`<div>I gave my ${d.color} ${d.animal}</div><div>${d.foods}</div>`;
  console.log(template);
});
```
>`<div>I gave my gray cat</div><div>fish,tuna,snack</div>`  
>`<div>I gave my black dog</div><div>nothing</div>`     

<br/>

## function  

### Arrow function의 this context  

es5 까지의 실행 컨텐스트에서 함수의 this는 전역 개체인 window를 가르킨다  
그래서 오브젝트 내의 함수에서 this가 해당 오브젝트를 가르키게 하려면 바인딩을 해줘야 했다  

```javascript
const x = {
  sayHello() {
    setTimeout(function() {
      this.hello();
    }.bind(this), 200);
  },
  hello() {
    console.log("hello everyone");
  }
}
x.sayHello();
```
>hello everyone  

<br/>

반면 es6의 arrow function의 this는 자신을 둘러 싼 환경의 this를 계승받는다  

```javascript
const x = {
  sayHello() {
    setTimeout( ()=> {
      this.hello();
    }, 200);
  },
  hello() {
    console.log("hello everyone");
  }
}
x.sayHello();
```
>hello everyone  

<br/>

### default parameters  

es5까지 함수에 default parameter를 넣는 법은 아래와 같다  

```javascript
function multiply(x, y) {
  y = y || 2;
  return x * y;
}
console.log(multiply(3, 5));
console.log(multiply(3));
```
>15  
>6  

<br/>

위 같은 방식은 파라미터 수가 늘어날 수록 앞쪽 선언부가 길어질 수 밖에 없다  
es6에서는 파라미터 부분에 다음과 같은 방식으로 설정할 수 있다  

```javascript
function multiply(x, y = 2) {
  return x * y;
}
console.log(multiply(3, 5));
console.log(multiply(3));
```
>15  
>6  

<br/>

Object 형태도 사용할 수 있다  


```javascript
function multiply(x, y = {value :2}) {
  return x * y.value;
}
console.log(multiply(3, {name: "size", value: 5}));
console.log(multiply(3));
```
>15  
>6  

<br/>

### rest parameters  

파라미터를 가변 개수로 받을 때, arguments를 파라미터에서 진짜 배열로 만들어 받을 수 있다  

```javascript
function checkNum(...argArr) {
  const result = argArr.every( (x) => typeof x === "number");
  console.log(result);
}
checkNum(1, 2, 3, "4", 5);
checkNum(10, 20, 30, 40, 50, 60, 70);
```
>false  
>true  

<br/>


