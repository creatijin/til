# 데이터 타입과 연산자

자바스크립트 타입

- 기본타입
  - 숫자(Number)
  - 문자열(String)
  - 불린값(Boolean)
  - undefined
  - null
- 참조타입
  - 객체( Object)
    - 배열(Array)
    - 함수(Function)
    - 정규표현식



####자바스크립트 기본 타입

~~~javascript
//숫자타입
var intNumber = 10; [1]
var floatNumber = 0.1; [1]

//문자열 타입
var single = 'single'; [2]
var dobule = "double"; [2]
var singleChar = 'a';

//불린타입
var boolVar = true; [3]

// undefined 타입
var emptyVar; [4]

// null 타입
var nullVar = null; [5]

console.log(
	typeof intNumber,
    typeof floatNumber,
    typeof single,
    typeof dobule,
    typeof boolVar,
    typeof nullVar,
    typeof emptyVar
);

//[출력결과]
number number string string boolean object undefined
~~~



### 숫자

자바스크립트는 하나의 숫자형만 존재한다.

자바스크립트 변수에는 정수나 실수 구분 없이 그 값을 바로 저장할 수 있으므로 intNumber, floatNumber 변수 모두 typeof 연산자의 결과값이 number타입이다.



**자바스크립트는 정수형이 따로 없고, 모두 숫자를 실수로 처리하므로 나눗셈 연산을 할때는 주의하자**

~~~javasvript
var num = 5/2;

console.log(num); // 2.5
console.log(Math.floor(num)); // 2
~~~

다른 언어(C언어)에서 할 경우 5/2는 소수 부분을 버린 2가 출력된다. 하지만 자바스크립트에서는 5/2 둘다 정수가 아닌 실수로 취급하므로 소수 부분까지 출력된 2.5가 결과값이다.

**소수 부분을 버린 정수 부분만을 구하고 싶다면 Math.floor() 메서드를 사용하자**



### 문자열

문자열은 ('),(")로 생성한다. 따라서 [2] 결과는 string 으로 나온다. **C언어의 char 타입과 같이 문자 하나만을 별도로 나타내는 데이터 타입은 존재하지 않는는다.**

**한번 정의된 문자열은 변하지 않는다.**

~~~javascript
// str 문자열 생성
var str = 'test';
console.log(str[0], str[1], str[2], str[3]);
//출력값 test

//문자열의 첫 글자를 대문자로 변경?
str[0] = 'T';
console.log(str); //출력값 test
~~~

자바스크립트의 문자열은 배열처럼 인덱스를 이용해서 접근할 수 있다.

str[0] 를 출력했을때 't'를 출력할 수 있다. 그리고 예제에서 str[0]을 't' > 'T' 를 대문자로 변경했지만 에러가 발생하지 않고 str를 출력했을때 'Test'가 아닌 'test'로 출력된다.

**자바스크립트에서는 한 번 생성된 문자열은 읽기만 가능하지 수정은 불가능하다**



### 불린값

true와 false 나 타내는 [3]에서 변수에 'true'로 값을 지정했으므로 boolean 타입이다.



### null and undefined

"null" 과 "undefined" 둘다 값이 비어있음을 나타낸다.

기본적으로 값이 할당되지 않는 변수는 undefined 타입이며, undefined 타입의 변수는 변수 자체의 값 또한 undefined 이다. **undefined는 타입이자, 값을 나타낸다.**

"null"의 경우 개발자가 명시적으로 값이 비어있음을 나타내는데 사용한다.

**주의** 할점은 null 타입 변수는 typeof 결과가 null이 아니라 object라는 것!!

Typeof 연산자를 사용하면 안되고, 일치 연산자(===)를 사용해서 변수의 값을 지정 확인 한다.

~~~javascript
//null 타입 변수 생성
var nullVar = null;

console.log(typeof nullVar === null) // false
console.log(nullVar === null) // true

~~~

