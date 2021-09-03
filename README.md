# javascript 정석 공부 

javascript를 기초부터 공부하면서 몰랐던 사실을 정리합니다  

- [데이터 타입](#데이터-타입)
  - [Number 타입의 숨겨진 세 가지](#Number-타입의-숨겨진-세-가지)
  - [Undefined 타입](#Undefined-타입)
  - [Object 타입](#Object-타입)


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


