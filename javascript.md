# javascript 정석 공부 

javascript를 기초부터 공부하면서 몰랐던 사실을 정리합니다  

- [데이터 타입](#데이터-타입)
  - [Number 타입의 숨겨진 세 가지](#Number-타입의-숨겨진-세-가지)
  - [Undefined 타입](#Undefined-타입)
  - [Object 타입](#Object-타입)
- [연산자](#연산자)
  - [연산 이전의 숫자 변환](#연산-이전의-숫자-변환)
  - [소수 값의 연산](#소수-값의-연산)
  - [== 연산자](#==-연산자)
  - [=== 연산자](#===-연산자)
  - [&&와 || 연산자의 반환값](#&&와-||-연산자의-반환값)  


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



