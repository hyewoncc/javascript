# javascript 정석 공부 

javascript를 기초부터 다시 공부하면서 **기존에 몰랐던 사실**을 정리합니다  
해당 문서는 **[인프런 자바스크립트 비기너 강의](https://inf.run/godD)** 를 수강하며 참고해 작성하였습니다  
ES6는 **[별도 문서](ES6.md)** 에 있습니다


- [데이터 타입](#데이터-타입)
  - [Number 타입의 숨겨진 세 가지](#number-타입의-숨겨진-세-가지)
  - [Undefined 타입](#undefined-타입)
  - [Object 타입](#object-타입)
- [연산자](#연산자)
  - [연산 이전의 숫자 변환](#연산-이전의-숫자-변환)
  - [소수 값의 연산](#소수-값의-연산)
  - [== 연산자](#-연산자)
  - [=== 연산자](#-연산자-1)
  - [&&와 || 연산자의 반환값](#와--연산자의-반환값)  
- [오브젝트](#오브젝트)  
  - [프로퍼티](#프로퍼티property)
  - [for~in문으로 프로퍼티 열거](#forin문으로-프로퍼티-열거하기)  
  - [프리미티브 값(Primitive Value)](#프리미티브-값primitive-value)  
- [Number](#number)
  - [toString(), toExponential(), toFixed()](#tostring-toexponential-tofixed)  
- [String](#string)
  - [length 프로퍼티와 반환 논리 / String 인스턴스의 구조](#length-프로퍼티와-반환-논리--string-인스턴스의-구조)  
- [Object](#objectes3)
  - [오브젝트 구분(네이티브/호스트)](#오브젝트-구분네이티브호스트) 
  - [Object의 인스턴스 생성](#object의-인스턴스-생성)  
  - [prototype?](#prototype)  
  - [함수와 메소드의 차이(ES5)](#함수와-메소드의-차이es5)  
  - [hasOwnProperty()](#hasownproperty)  
- [Function](#function)  
  - [함수 선언문과 함수 표현식](#함수-선언문과-함수-표현식)  
  - [call(), apply()](#call-apply)  
- [Global](#global)  
  - [Global과 Window의 관계](#global과-window의-관계)  
- [Array(ES3)](#arrayes3)  
  - [Array의 콜백 함수를 쓰는 프로퍼티들](#array의-콜백-함수를-쓰는-프로퍼티들)  
  - [forEach()](#foreach)  
  - [reduce()](#reduce)  
- [Object(SE5)](#objectse5)  
  - [Object에 프로퍼티 추가](#object에-프로퍼티-추가)  
  - [프로퍼티 디스크립터](#프로퍼티-디스크립터)  
  - [프로퍼티 추출](#프로퍼티-추출)  
  - [프로퍼티 디스크립터 함수](#프로퍼티-디스크립터-함수)  




<hr/>


## 데이터 타입 

### Number 타입의 숨겨진 세 가지  

자바스크립트의 Number 타입에는 특수한 세 가지 값이 있다  
1. 양의 무한대 Infinity 
2. 음의 무한대 -Infinity
3. Not a Number인 NaN

```javascript
var x = 10 * "Hello";
console.log(x)
```
>NaN

Number와 문자열의 곱이기에 오류가 나지만  
코드가 정지되지는 않고 마저 실행되며, NaN 이라는 값이 담기게 된다  

<br/>

### Undefined 타입
값은 소문자로 시작하는 undefined 이다   
변수를 선언하면 초깃값으로 undefined가 설정되고 직접 할당도 가능하다  
하지만 초깃값인지 할당한 것인지 구분이 불가하므로 권장하지 않고 null을 할당하는 게 낫다  
```javascript
var x;
console.log(x);
```
>undefined

<br/>

### Object 타입  
자바스크립트의 기본 구조로 {name : value} 형태이다  
둘을 묶어서 하나의 쌍을 프로퍼티(property)라고 지칭한다  
Object를 프로퍼티의 집합이다  
name은 key라고 부르기도 한다  

```javascript
var cat = {
  color: "gray", sound: "meow", foot: 4
};
console.log(cat);
```
>{color: "gray", sound: "meow", foot: 4}

<br/>

## 연산자

### 연산 이전의 숫자 변환  
자바스크립트는 연산하지 전에 우선 숫자로 변환 후에 변환 값으로 연산한다  

|값 타입|변환 값|
|:---:|:---:|
| Undefined | NaN |
| Null | +0 |
| Number | 변환 전/후 같음 |
| String | 값이 숫자면 숫자 연산 <br/> 단, 더하기(+)는 연결 |  

다음은 연산 이전의 변환을 보여주는 예시들이다  

```javascript
var x;
console.log(10 + x);
```
>NaN  
>x가 undefined 이므로 더한 값도 NaN이 된다  

<br/>

```javascript
console.log(123 + "45");
console.log(123 - "45");
```
>12345  
>78  
>더하기(+) 연산은 문자열로 연결, 다른 연산자는 숫자로 변환 처리  

<br/>

### 소수 값의 연산  

IEEE 754 유동 소수점 처리를 따르기에 소수점 연산에 주의해야한다  

```javascript
console.log(2.3 * 3);
```
>6.8999999999999995  

<br/>

이처럼 기대한 값인 6.9가 나오지 않는 것을 볼 수 있지만 이것이 정상이다  
실수를 정수로 변환하여 값을 구하고 다시 실수로 변환하면 6.9를 얻을 수 있다  

```javascript
console.log(2.3 * 10 * 3 / 10);
```
>6.9  

<br/>

이는 나머지 연산에도 적용된다  

```javascript
console.log(5 % 2.4);
```
>0.20000000000000018  

<br/>

기대한 값인 0.2가 나오도록 하려면 역시나 정수로 변환해 값을 구하고 다시 변환해야 한다  

```javascript
console.log((5 * 10 - ( 2 * 2.4 * 10)) / 10 );
```
>0.2  

<br/>

### == 연산자  
동등 연산자로 왼족과 오른쪽 '값'이 같으면 true, 아니면 false를 반환한다  
값 '타입'은 비교하지 않는 것에 유의한다  

```javascript
console.log(1.2 == "1.2");
```
>true  

<br/>

단, 예외로 undefined와 null을 비교할 시 값이 다름에도 true가 된다  

```javascript
var x;
console.log(x == null);
```
>true  

<br/>

### === 연산자  
일치 연산자로 왼쪽과 오른쪽의 '값'과 '타입'이 모두 같아야 true를 반환하다  

```javascript
console.log(1.2 === "1.2");
```
>false  

<br/>

undefined와 null은 동등 연산자로는 true를, 일치 연산자로는 false를 반환한다  

```javascript
var x;
console.log(x == null);
console.log(x === null);
```
>true  
>false  

<br/>

### &&와 || 연산자의 반환값     

논리 AND 연산자는 평과 결과가 둘 다 true면 true, 아니라면 false가 된다  
왼쪽 결과가 false라면 남은 오른쪽은 비교하지 않는다  
논리 OR 연산자는 평과 결과가 하나라도 true면 true, 아니라면 false가 된다  
왼쪽 결과가 true라면 남은 오른쪽은 비교하지 않는다  
반환값은 true/false가 아니라 **true/false가 되는 마지막 변수값**이 된다  

```javascript
var x, y = 0, z = 2;
console.log(x || y || z);
```
>2  
>먼저 undefined인 x와 0인 y를 처리하여 false  
>후에 z가 2이므로 true가 되며, 변수값으로는 z의 값인 2는 반환  

<br/>


## 문장  

### 세미콜론 자동 삽입  

세미콜론 없이 문장을 끝내고 줄을 분리(화이트 스페이스 삽입)했다면 엔진이 자동으로 삽입해준다  
한 줄에 이어서 작성하면 삽입하지 않는다  

```javascript
var x = 1
var y = 2
console.log(x + y)
```
>3  
>에러가 나지 않는 것은 줄바꿈으로 각 줄 끝에 세미콜론이 삽입되었기 때문  

<br/>

### strict 모드  

"use strict"를 사용하면 JS 문법을 엄격하게 사용하도록 선언할 수 있다  
작성한 위치부터 적용된다  

```javascript
x = "고양이";
console.log(x);
```
>고양이  
>변수 선언자(var, let, const)를 빼먹었지만 "고양이"가 할당되었다  

<br/>

```javascript
"use strict";
try {
  x = "고양이";
  console.log(x);
} catch(error){
  console.log(error.message);
}
```
>x is not defined
>변수 선언자가 없기에 에러가 발생해서 catch 구문이 실행되었다  

<br/>

## 오브젝트  

### 프로퍼티(property)  

{name : value} 형태로 이루어져 있다  
value에는 다양한 값이 들어갈 수 있는데, 객체와 함수를 포함한다  

```javascript
var cat = {
  color: "gray",
  habit: {
    sleep: 20,
    eat: 3,
    act: meow(){}
  }
}
```  

<br/>

오브젝트에 프로퍼티를 추가하거나 변경할 수 있다  
없는 name이라면 추가되고, 있는 name이라면 값이 변경된다  
방식은 세 가지가 있다  

```javascript
var cat = {};

// object.name = value 형태  
cat.color = "gray";

// object[name] = value 형태  
cat.foot = 4;

// ojbect[변수 이름] = value 형태  
var key = "color";
cat[key] = "yellow";

console.log(cat);
```

>{color: "yellow", foot: 4}  

<br/>

### for~in문으로 프로퍼티 열거하기  

for (변수 in 오브젝트) 또는 for (표현식 in 오브젝트)로 프로퍼티를 열거할 수 있다  
프로퍼티를 작성한 순서대로 읽힌다는 걸 보장하지 않으나 ES5부터는 보장된다   

```javascript
var animals = {
  cat: "고양이",
  dog: "개",
  parrot: "앵무새"
};

for (var animal in animals){
  console.log(animal);
  console.log(animals[animal]);
}
```

>cat  
>고양이  
>dog  
>개  
>parrot  
>앵무새  

<br/>

### 프리미티브 값(Primitive Value)  

프리미티브 값이란 가장 낮은 단계의 값을 의미한다
var cat = "고양이"; 가 있을 때, "고양이"는 더이상 분해하거나 전개할 수 없다  
따라서 "고양이"는 프리미티브 값이다  
프리미티브 타입 중 Number, String, Boolean은 인스턴스 생성이 가능하고,  
Null, Undefined는 인스턴스 생성이 불가하다  
Object는 프리미티브 값을 제공하지 않는다  

```javascript
var cat = "고양이";
var drink = "커피";
```

<img width="139" alt="스크린샷 2021-09-04 오후 6 50 29" src="https://user-images.githubusercontent.com/80666066/132090328-52cbeb37-a653-419e-9a20-1b410968a9e4.png"> <img width="160" alt="스크린샷 2021-09-04 오후 6 50 24" src="https://user-images.githubusercontent.com/80666066/132090329-77c7ba29-be54-4f75-b3dd-4c3b100581e3.png">  

"고양이"와 "커피"는 프리미티브 값이다  

<br/>

```javascript
var study = {lang : "자바스크립트"};
```

<img width="285" alt="스크린샷 2021-09-04 오후 6 56 00" src="https://user-images.githubusercontent.com/80666066/132090431-2b460348-f6b5-42b3-9194-7183815a56b0.png">

Object의 인스턴스에는 프리미티브 값이 존재하지 않는다  

<br/>

```javascript
var score = new Number(100);
console.log(score + 100);
```  
>200  

<img width="318" alt="스크린샷 2021-09-04 오후 6 57 34" src="https://user-images.githubusercontent.com/80666066/132090483-bcf1e0eb-b069-481e-9b39-9ef598277257.png">

반면 Number의 인스턴스에는 자바스크립트 엔진이 자동으로 대괄호 안에 PrimitiveValue로 파라미터의 값을 저장한다  
score는 인스턴스므로 원래 값을 더할 수 없는데, 100이 프리미티브 값으로 자동 설정되었기에 가능하다  
프리미티브 값을 갖는 인스턴스에 연산을 실행하면 값이 계산된다  
valueOf()로 Number 인스턴스의 프리미티브 값을 반환받을 수 있다  

<br/>

## Number

### toString(), toExponential(), toFixed()  

toString()은 data를 String 타입으로 변환한다  
주의할 점은, IEEE 754 유동 소수점 처리를 따르기에 정수를 변환할 때 점을 두 개 붙여야 한다는 것이다  
10.toString()의 경우 20. 까지를 수로 인식하기에 10..toString()이 되어야 한다  

```javascript
console.log(10.toString());
console.log(10..toString());
```
>Uncaught SyntaxError: Invalid or unexpected token (윗줄만 실행)  
>10 (아랫줄만 실행)  

<br/>

toExponential()은 숫자를 지수 표기로 변환한 문자열을 반환한다  
첫 자리만 소수점 앞에 표시되고, 정수에서 소수로 변환된 자릿수가 지수 뒤에 붙는다  
선택적으로 파라미터에 몇 자리 까지 작성할 지 지정할 수 있으며, 아래 자리에서 반올림한다  

```javascript
var x = 12345;
console.log(x.toExponential());
x = 123456;
console.log(x.toExponential(4));
```
>1.2345e+4  
>1.2346e+5  
>
<br/>

toFixed()는 숫자를 고정 소숫점 표기로 변환한 문자열을 반환한다  
파라미터로 반환할 소수 이하 자릿수를 정할 수 있고, 적지 않으면 0으로 간주된다  
변환 대상 자릿수보다 파라미터 값이 크면, 남은 자리를 0으로 채워 반환한다  

```javascript
var x = 1234.5678;
console.log(x.toFixed(2));
console.log(x.toFixed());
console.log(x.toFixed(7));
```
>1234.57  
>1235  
>1234.5678000  

<br/>

## String  

### length 프로퍼티와 반환 논리 / String 인스턴스의 구조  

String의 인스턴스에는 문자열 길이를 나타내는 length 프로퍼티가 있다  
그런데 인스턴스가 아닌 문자열도 length 값을 쓸 수 있는데,  
이는 자바스크립트 엔진에서 .length를 만나면 내부에서 new String으로 인스턴스를 자동 생성하기 때문이다  

```javascript
var c = "cat";
console.log(c.length);
var d = new String("dog");
console.log(d.length);
```
>3  
>3  

<img width="137" alt="스크린샷 2021-09-04 오후 9 41 48" src="https://user-images.githubusercontent.com/80666066/132094797-aa2912e4-0105-434b-9f51-60fa9b6482b7.png"> <img width="248" alt="스크린샷 2021-09-04 오후 9 41 53" src="https://user-images.githubusercontent.com/80666066/132094802-e89cbb17-f6eb-46b7-8024-46feb43c8932.png">  
이처럼 c는 인스턴스가 아니지만 length로 3 값이 있다  
또, d를 살펴보면 문자열이 인스턴스에 d,o,g로 하나씩 분리되어  
각각 인덱스 값에 따른 프로퍼티로 저장되어 있는 것을 볼 수 있다  

<br/>

## Object(ES3)  

### 오브젝트 구분(네이티브/호스트)  

자바스크립트의 오브젝트는 크게 네이티브/호스트의 두 가지로 나눌 수 있다  

- 네이티브는 JS 스펙에서 정의한 오브젝트이다  
  Number, String 같은 빌트인 오브젝트를 포함한다  
  JS 코드를 싫애할 때 만들어 진다 (예: Argument)
- 호스트는 빌트인, 네이티브를 제외한 모든 오브젝트이다  
  window, DOM 등이 여기에 속한다  
  
<br/>

### Object의 인스턴스 생성  

new Object()로 생성한 인스턴스는 파라미터의 데이터 타입에 따라 생성할 인스턴스가 결정된다  
파라미터 값이 undefiend, null이면 빈 Object 인스턴스가 반환된다  

```javascript
var objectX = new Object(100);
console.log(objectX + 100);
var objectY = new Object();
console.log(objectY);
```
>200  
>{}  

숫자 100을 넣어 생성한 objectX에 숫자와의 연산이 되므로 ojbectX는 Number 타입이다  

<br/>

Object()로 생성한 인스턴스는 {name: value} 형태의 파라미터로 생성할 수 있다  
역시나 파라미터가 빈다면 빈 Object의 인스턴스가 반환된다 (new Object()와 같다)  
또, 변수 = {} 형태로도 빈 Object를 만들 수 있다  
{}를 오브젝트 리터럴(Literal)이라 부른다  

```javascript
var objectX = Object({dog: "bark"});
console.log(objectX);
var objectY = Object();
console.log(objectY);
var objectZ = {};
console.log(objectZ);
```
>{dog: "bark"}  
>{}  
>{}  

<br/>

### prototype?

프로토타입을 간단하게 정리하자면 다음과 같다  
- 오브젝트.prototype이 있어야 인스턴스 생성이 가능하다  
  예시로 계산용 오브젝트인 Math는 프로토타입이 존재하지 않는다  
  prototype은 프로퍼티를 연결하는 오브젝트이다  
  예를 들어 오브젝트.prototype.constructor는 오브젝트의 생성자를 연결한다  
  
<br/>

### 함수와 메소드의 차이(ES5)  

- 함수는 오브젝트에 연결한다
  ex) Object.create()
- 메소드는 프로토타입에 연결한다  
  ex) Object.prototype.toString()
t 
ES5 공식 문서에서는 function과 method를 위와 같이 구분하고 있다  
함수는 파라미터에 값을 작성하고, 메소드는 메소드 앞에 값을 작성한다  

<br/>

### hasOwnProperty()  

hasOwnProperty() 메소드는 인스턴스에 파라미터 이름이 프로퍼티로 존재하면 true를, 아니라면 false를 반환한다  
상속받은 프로퍼티면 false를 반환하는 것에 주의한다  

```javascript
var objectX = {};
console.log(objectX.hasOwnProperty("hasOwnProperty"));
```
>false  

{hasOwnProperty : hasOwnProperty()}는 인스턴스 자신에 있는 것이 아니라 Object에서 상속 받은 것이다  

<br/>

## Function  

### 함수 선언문과 함수 표현식  

함수 선언문은 function getPlus(n, m){return n+m;};   
함수 표현식은 var getPlus = function(n, m){return n+m;}; 형식이다  

```javascript
function getPlus1(n, m){
  return n + m;
};
var x = getPlus1(2, 3);
console.log(x);

var getPlus2 = function(n, m){
  return n + m;
};
var y = getPlus2(3, 4);
console.log(y);
```
>5  
>7  

함수 표현식에서 var getPlus = function plus(n, m){return n+m;}; 식으로도 작성 가능하고,  
이 때 plus를 식별자라 하는데 생략 가능하다  
둘은 같아보이나 함수 선언문이 함수 표현식보다 먼저 실행(=Function 오브젝트 생성)되는 차이가 있다  

<br/>

### call(), apply()  

object.call()은 함수를 호출하는 메소드며 파라미터 수가 고정일 때 사용한다  
첫 번째 파라미터로 this로 참조할 오브젝트를 받고, 옵션으로 호출된 함수로 넘길 파라미터를 넣는다  

```javascript
function getPlus(n, m) {
  return n + m;
};
var x = getPlus.call(this, 2, 3);
console.log(x);
```
>5  
이 예시는 첫 번째 파라미터인 this가 파라미터 값으로 넘어가지 않는 예시이다  

<br/>

```javascript
var nums = {n : 3, m : 4};
function getPlus() {
  return this.n + this.m;
};
var y = getPlus.call(nums);
console.log(y);
```
>7  
이 예시는 첫 번째 파라미터가 nums 오브젝트를 참조하기에 this로 프로퍼티에 접근해 값을 구한다  

<br/>

object.apply()는 역시 함수를 호출하는 메소드지만, 파라미터 수가 유동적일 때 사용한다  
첫 번째 파라미터로 this를, 옵션으로 호출된 함수로 넘길 파라미터를 배열로 넣는다  

```javascript
function getPlus(n, m){
  return n + m;
};
var x = getPlus.apply(this, [5, 6]);
console.log(x);
```
>11  

<br/>

## Global

### Global과 Window의 관계  

Global 오브젝트는 JS가 주체인 반면, window 오브젝트는 window가 주체다  
하지만 Global 오브젝트는 실체가 없으므로 Global 오브젝트의 프로퍼티와 함수는 window 오브젝트에 설정되며,  
Global 오브젝트의 프로퍼티를 window에서 가져오면 된다  

<br/>

## Array(ES3)

### sort()  

배열의 sort() 메소드는 숫자 배열을 정렬 할 경우 숫자에 해당하는 Unicode의 code point로 정렬한다  
이는 수의 크기 순으로 정렬되지 않을 수 있다는 뜻이다  

```javascript
var arr = [120, 25, 8, 1300];
console.log(arr.sort());
```
>[120, 1300, 25, 8]  

보시다시피, 8, 25, 120, 1100 순으로 나오지 않는다  
이는 숫자의 맨 앞자리부터 비교하여 정렬하기 때문이다  
숫자를 크기순으로 정렬하고 싶다면 파라미터로 콜백 함수를 작성해 넣어야 한다 

<br/>

```javascript
var arr = [120, 25, 8, 1300];
arr.sort(function(n, m){
  return n - m;
});
console.log(arr);
```
>[8, 25, 120, 1300]  

return m - n 으로 하면 이를 역순 정렬할 수 있다  

<br/>

## Array(ES5)  

### Array의 콜백 함수를 쓰는 프로퍼티들  

아래의 일곱개 메소드는 모두 콜백 함수를 실행한다  

- forEach() : 배열을 순회하며 콜백 함수 실행  
- every() : 반환 값이 false 일 때 까지 순회하며 콜백 함수 실행  
- some() : 반환 값이 true일 때 까지 순회하며 콜백 함수 실행  
- filter() : 반환 값이 true인 엘리먼트 반환  
- map() : 콜백 함수에서 반환한 값을 새로운 배열로 반환  
- reduce() : 콜백 함수의 반환 값을 파라미터로 사용  
- reduceRight() : reduce()와 같으나 배열 역순으로 진행  

<br/>

### forEach()  

forEach()의 콜백 함수는 다음과 같은 형태로 작성한다  
function(해당 엘리먼트, 인덱스, 전체 배열){}

```javascript
var x = ["A", "B", "C"];
x.forEach(function(e, index, arr){
  console.log(e + " is " + index + " in " + arr);
});
```
>A is 0 in A,B,C  
>B is 1 in A,B,C  
>C is 2 in A,B,C

<br/>  

또한, this로 오브젝트를 참조할 수 있다  
이 오브젝트는 파라미터로 넘어가지는 않는다  

```javascript
var x = [1, 2, 3, 4];
var multiplyNine = function(e, index, arr){
  console.log(e * this.nine);
};
x.forEach(multiplyNine, {nine: 9});
```
>9  
>18  
>27  
>36  

<br/>

forEach()는 시작할 때 반복 범위를 결정하기에, 중간에 엘리먼트를 추가해도 처리되지 않는다  
```javascript
var x = [1, 2, 3];
x.forEach(function(e, index, arr){
  x.push(4);
  console.log(e);
});
console.log(x);
```
>1  
>2  
>3  
>[1, 2, 3, 4, 4, 4]  

4가 세 개 추가되었지만, 콜백 함수 실행 중엔 출력되지 않는 것을 볼 수 있다  
하지만, 현재 인덱스 보다 큰 인덱스의 값을 변경하거나 삭제하면 그건 반영이 된다    

```javascript
var x = [1, 2, 3, 4, 5];
x.forEach(function(e, index, arr){
  x[2] = 7;
  x.pop();
  console.log(e);
});
```  
>1  
>2  
>7  

<br/>

for문과 비교해 forEach()는 시맨틱 접근의 의미를 갖는데, 아래 함의를 갖고 있기 때문이다  
- 처음부터 끝까지 반복(중간에 끝나지 않음)  
- 기능 처리는 콜백 함수에서 하며, this 사용 가능  
- 인덱스 증가 값의 조정 불가  
- 앞에서 뒤로 가는 단방향만 가능  

<br/>

### reduce()  

reduce()는 배열 끝까지 콜백 함수를 호출하는데, 반환 값을 다시 파라미터로 사용한다  

```javascript
var x = [1, 2, 3, 4];
var result = x.reduce(function(pre, crr, index, arr){
  console.log(pre + " and " + crr);
  return pre + crr;
});
console.log(result);
```
>1 and 2  
>3 and 3  
>6 and 4  
>10  

첫 pre는 x[0]의 값이 들어갔지만, 그 다음 부터는 앞서 얻은 return 값이 들어감을 볼 수 있다  
첫 시작 인덱스가 1이 되기 때문에, 네 번이 아니라 세 번 반복한다  

<br/>

두 번째 파라미터가 있는 경우, 해당 파라미터를 첫 번째 pre로 설정한다  

```javascript
var x = [1, 2, 3, 4];
var result = x.reduce(function(pre, crr, index, arr){
  console.log(pre + " and " + crr);
  return pre + crr;
}, 100);
console.log(result);
```
>100 and 1  
>101 and 2  
>103 and 3  
>106 and 4  
>110  

이 경우는 네 번 반복하는 것을 볼 수 있다  
reduceRight()는 전부 동일하나, 배열의 뒤에서 앞으로 진행된다  

<br/>


## Object(SE5)  

### Object에 프로퍼티 추가  

defineProperty()로 대상 오브젝트에 프로퍼티를 추가하거나 속성을 변경할 수 있다  
프로퍼티마다 변경/삭제/열거 가능 여부 상태를 갖고 있으며, 가능일 때만 해당 처리를 할 수 있다  
이 상태는 프로퍼티를 추가할 때 결정하게 된다  
첫 번째 파라미터에 프로퍼티를 추가할 대상 오브젝트를,  
두 번째 파라미터에 프로퍼티 이름을,  
세 번째 파라미터에 {value: 값}을 넣어 해당 프로퍼티 값을 설정한다  

```javascript
var cat = {};
Object.defineProperty(cat, "species", {
  value: "cat",
  enumerable: true
});
console.log(cat);
```
>{species: "cat"}  

<br/>  

defineProperties()는 다수의 프로퍼티를 추가, 변경하며 기능은 defineProperty()와 동일하다  

```javascript  
var cat = {};
Object.defineProperties(cat, {
  species: {
    value: "cat", enumerable: true
  },
  sound: {
    value: "meow", enumerable: true
  },
  food: {
    value: "meat", enumerable: false 
  }
});
for (var name in cat){
  console.log(name + " : " + cat[name]);
};
console.log(cat);
```
>species : cat  
>sound : meow  
>{species: "cat", sound: "meow", food: "meat"}  

세 개의 프로퍼티 값이 정상적으로 설정 되었고,  
enumerable을 false로 설정한 food만 for문에서 돌지 않아 출력되지 않음을 볼 수 있다  

<br/>

### 프로퍼티 디스크립터  

프로퍼티의 속성 이름과 값을 정의하는 함수이다  
같은 타입에 속한 속성만 같이 사용할 수 있다  

| 타입  | 속성 이름 | 디폴트 값 | 기능  |
|:---:|:---|:---|:---|
| 데이터 | value | undefined | 프로퍼티 값  |
| 데이터 | writbale  | false | value 값 변경 가능 여부 |
| 엑세스 | get | undefined | 프로퍼티 값 반환 |
| 엑세스 | set | undefined | 프로퍼티 값 설정 |
| 공용  | enumerable  | false | for-in 열거 가능 여부 |
| 공용  | configurtalbe | false | 프로퍼티 삭제 가능 여부 |  

<br/>

### 프로퍼티 추출  

getPrototypeOf()로 파라미터 인스턴스의 프로퍼티를 반환받을 수 있다  

```javascript
function Dog(sound){
  this.sound = sound;
};
Dog.prototype.getSound = function(){};
Dog.prototype.setSound = function(){};

var obj = new Dog("bark");
var result = Object.getPrototypeOf(obj);
console.log(result);
```
>{getSound: ƒ, setSound: ƒ, constructor: ƒ}  

<br/>

getOwnPropertyNames()로 파라미터 오브젝트의 프로퍼티 이름들의 배열을 반환받을 수 있다  
열거 가능 여부를 체크하지 않으며, 자신이 만든 프로퍼티만 대상이다  

```javascript
var dog = {};
Object.defineProperties(dog, {
  color: {
    value: "black",
    enumerable: true
  },
  sound : {
    value: "bark",
    enumerable: false
  }
});
var names = Object.getOwnPropertyNames(dog);
console.log(names);
```
>(2) ["color", "sound"]  

color만 열거 가능이고, sound는 열거 불가를 설정헀는데 둘 다 배열에 들어온 것을 볼 수 있다  
<br/>

반면 keys()는 열거 가능 프로퍼티만 반환해준다  

```javascript
var dog = {};
Object.defineProperties(dog, {
  color: {
    value: "black",
    enumerable: true
  },
  sound : {
    value: "bark",
    enumerable: false
  }
});
var names = Object.keys(dog);
console.log(names);
```
>["color"]  

<br/>  


### 프로퍼티 디스크립터 함수  

getOwnPropertyDescriptor()로 해당 프로퍼티의 디스크립터를 반환받을 수 있다  
getOwnPropertyNames()와 마찬가지로 다른 오브젝트에서 받은 프로퍼티는 제외된다   

```javascript
var dog = {};
Object.defineProperties(dog, {
  color: {
    value: "black",
    enumerable: true
  },
  sound : {
    value: "bark",
    writable:true, enumerable: false
  }
});
var result = Object.getOwnPropertyDescriptor(dog, "sound");
console.log(result);
```
>{value: "bark", writable: true, enumerable: false, configurable: false}  

<br/>

preventExtensions()로 프로퍼티 추가 금지를 설정하고, isExtensible()로 금지 여부를 반환받을 수 있다  
프로퍼티 삭제, 변경은 가능하며, 설정 후에는 가능으로 변경이 불가하다  

```javascript
var dog = {};
Object.preventExtensions(dog);
try{
  Object.defineProperty(dog, "color", { value: "dart" });
} catch (e) {
  console.log("추가 불가");
};
console.log(Object.isExtensible(dog));
```
>추가 불가  
>false  

<br/>

seal()로 오브젝트에 프로퍼티 추가 및 삭제 금지를 설정하고, isSealed()로 금지 여부를 반환받을 수 있다  
프로퍼티 값 변경은 가능하다  

```javascript
var parrot = {};
Object.defineProperty(parrot, "color", {
  value: "rainbow", writable: true
});

Object.seal(parrot);
try{
  Object.defineProperty(parrot, "speak", {
    value: true
  });
} catch(e) {
  console.log("추가 불가");
};
console.log(Object.isSealed(parrot));
```
>추가 불가  
>true  

<br/>

freeze()로 오브젝트 프로퍼티에 추가, 삭제, 변경 금지를 설정하고, isFrozen()으로 금지 여부를 반환 받을 수 있다  

```javascript
var frog = {};
Object.defineProperty(frog, "doing", {
  value: "jumping", writable: true
});
Object.freeze(frog);

try {
  Object.defineProperty(frog, "doing", {
    value: "singing"
  });
} catch(e) {
  console.log("변경 불가");
};
console.log(Object.isFrozen(frog));
```
>변경 불가  
>true  

<br/>
