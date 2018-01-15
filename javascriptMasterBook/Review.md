# 자바스크립트 마스터북(기초부터 실무 응용까지)
> 2018.01.14 읽음. 양이 많다. 그러므로 모르는 것만 기록하겠다.
## 1장
특별한 내용 없음
## 2장
* 모두 그런것은 아니지만 일반적으로 표기할 때
    * 변수명이나 함수명 - camelCase
    * 상수명 - 언더스코어
    * 클래스(생성자)명 - pascal
* 연속적으로 `'`를 쓰고 싶다면 `\(이스케이프 시퀀스)`를 이용하세요
* null과 undefined는 확실하게 구분이 되어있습니다. 적절하게 사용하세요.
    * `undefined`
        * 어떤 변수가 선언완료 상태에서 값을 부여하지 않은 경우 
        * 미정의된 프로퍼티를 참조하려는 경우
        * 함수의 반환값이 없는 경우
        * 본래 참조할 의도가 없었을 때 많이 사용한다.
    * `null`
        * 객체가 존재하지 않는 것
        * 비어있다 그 자체의 의미, 주로 의도적으로 빈 값(빈 객체)를 표현할 때 쓴다.
* 소수점의 연산은 항상 주의해야한다(어느 언어든)
    * `0.2*3 === 0.6` 의 결과는 false일 것이다.
        * 그럼 어떻게 비교할까?
            * 정수로 만들어서 계산하든지..
            * 원하는대로..
* 상수는 `재대입`이 불가능하다.
    * 여기서 중요한 것이 있는데 배열, 객체, 함수들이 어떻게 작동하는 지 봐야한다.
    * 일단 ES6에서는 상수에 `const`란 키워드를 사용한다.
    * 밑 경우를 본다면 재대입이 안된다는 의미를 알 수 있을 것이다.
```js
const TAX = 101;
TAX = 200; // ERROR o 
const arr = [1,2,3,4];
arr[1] = 2; // ERROR x
arr = [2,3,4,5]; // ERROR o 
const obj = {1: "err", 2:"noERR?"};
obj[1] = "NO"; // ERROR x
obj = {1: 222, 2:333}; // ERROR o
```
* 바꾸기(ES6 이후)
```js
let a = 1;
let b = 2;
[a, b] = [b, a]; // swap
```
* delete연산자는 참조를 끊는 것이지 값을 삭제하는 것은 아니다.
```js
let a = 1;
delete a; // false -> 명시적으로 선언한 값 자체를 삭제하는 것은 불가능하다.
```
* 이 중괄호는 어떤 결과를 낳을까?
```js
var x = 1;
var y = 2;
if (x===1)
    if(y==2)
        console.log('x,y는 1,2이다');
else
    console.log('x는 1이 아니다');
```
이 결과는 `x는 1이 아니다`가 출력이 된다. 중괄호를 생략할 경우 개행으로 판단하는 것이 아니라 가장 가까이 있는 else로 나타나게 된다. 아무튼 결과론 적으로는 중괄호를 잘 쓰자
* switch
자바스크립트에는 `==`과 `===`이 존재합니다. switch에서 case값을 비교할 떄는 `===`을 사용합니다. 
* for - in 명령은 배열에서 사용할 기능이 아닙니다.
    * for-in 명령은 처리의 순서를 보증하지 않을 뿐더러
    * 가변수에는 인덱스 번호가 담길 뿐이므로 그 값자체가 아니기 떄문에 오해를 불러 일으킵니다.
    * 고로 for-of를 이용하자
* for - of는 단순히 모든 object의 값을 순회할 수 있는 것이 아닙니다. 배열처럼 iterable object인 것을 순회할 때 주로 사용하게 됩니다. 
* Strict 모드
    * JavaScript자체의 불완전한 특성들을 보완하기 위해 그런 코드를 오류로 방지하기 위한 모드이다.
    * 그냥 파일이나 그 함수 내에서 `'use strict'`를 작성하면 사용이 되는 것이다.
    * Strict 모드에 의해 주로 제한 되는 것을 보면
        * `var`의 생략
        * 인수 / 프로퍼티명 중복
        *  `null`, `undefined`를 대입
        *  `with` 명령어 사용 등등 이 있다.
    * 예제 코드를 보자
```js
'use strict'
try{
    a = 1; // var를 생략했다.
    console.log(a);
} catch(e){
    console.log(e.message);
}
```
결과는 a is not defined가 출력된다. Strict하게 검사를 하는 것이다.

## 3장
* Boolean 생성자로 생성한 객체는 무조건 true이다
```js
var flag = new Boolean(false);
console.log(flag); // true
```
* `startsWith`를 간단하게 살펴보면
```js
let str = "Hello world";
str.startsWith("Hello"); // true
str.startsWith("Hell"); // true
str.startsWith("Hello", 1); // false
str.startsWith("Hello", 0); // true
```
* `substring`, `slice`, `substr` 메소드를 비교해보자
    * start > end 일 경우 substring의 경우 end+1 ~ start로 바꿔서 출력
    * slice는 그대로
    * start 혹은 end가 음수일 경우 substring의 경우 0으로
    * slice는 뒤에서부터 셈(ex> -2일 경우 뒤에서 세번째 인덱스가 된다.)
```js
let str = "WINGS프로젝트";
console.log(str.substring(8,5)); // 프로젝
console.log(str.substr(8,5)); // 트
console.log(str.slice(8,5)); // 

console.log(str.substring(5,-2)); // WINGS
console.log(str.substr(5,-2)); // 
console.log(str.slice(5, -2)); // 프로
```
* 자바스크립트의 Number 객체
    * 자바스크립트에서 최대 save integer는 `2^53 - 1`이다. 고로 64비트를 표현하려면 어떻게 해야할까?
        * BigNumber나 Int64 라이브러리 사용해서 나타내야지..
* 값의 타입 변환
```js
console.log(typeof(123+'')); // string
console.log(typeof('123'-0); // number
console.log(typeof('123'-'0'); // number
console.log(typeof('123'-4)); // number(119가 된다.)
```

### Symbol(ES2015)
* Symbol은 Number, Boolean처럼 새롭게 추가된 자바스크립트 Primitive value값이다.
* 어느 블로그에나 있는 if(Symbol("a") === Symbol("b")) {...} 는 당연히 false일 것이다.
    * 매번 다른 해시값을 생성한다고 한다.
* 어디에 쓸까...감이안온다. 물어보자!

다시 돌아와서 
* Array를 stack과 queue처럼 쓰려면 어떻게 할까?
```js
// stack 은 push pop
let st = new Array();
st.push(1);
st.push(2);
st.push(3);
console.log(st.pop()); // 3
console.log(st.pop()); // 2
console.log(st.pop()); // 1
console.log(st.length); // 0
// queue 는 push shift
let qu = new Array();
qu.push(1);
qu.push(2);
qu.push(3);
console.log(qu.shift()); // 1
console.log(qu.shift()); // 2
console.log(qu.shift()); // 3
console.log(qu.length); // 0 
```
* 세트로 알아두자
```js
let data = [100,200,300];
data.forEach((val)=>{
    console.log(val);
});
data.forEach((val,idx,arr)=>{
    console.log(val,idx,arr);
});
data.map((val)=>{
    console.log(val);
});
data.map((val,idx)=>{
    console.log(val,idx);
});
let result = data.filter((val)=>{
    return val%2 == 0;
});

console.log(result); // [200, 300]
```

### Map과 Set
일반적으로 C++ 스탠다드 라이브러리에서 사용했었던 맵, 셋과 특성이 비슷하다.
여기서 Map은 연상배열로 해시처럼 작동하며 Set은 중복되지 않은 값들이 들어간다.
그럼 여기서 의문이 들 수 있다. Object와 Map의 차이는 그럼 뭘까.

* Map과 객체 리터럴과의 차이
    * 임의의 형으로 키를 이용할 수 있다. Nan혹은 객체 또한 키가 될 수 있다.
    * 맵의 사이즈를 취득할 수 있다.
    * 클린 맵을 만들 수 있다. 
        * create를 사용하여 Object를 만들어 클린하게 만들 수 있지만 굳이 그럴 필요 없이 Map을 쓰지
    * 

--- 2018.01.15

## 4장
## 5장
## 6장