# 자바스크립트 참조 타입(객체 타입)

숫자, 문자열, 불린값, null, undefined 같은 기본 타입을 제외한 모든 값은 객체다.

배열, 함수, 정규표현식 등도 모두 자바스크립트 객체로 표현된다.

**객체는 단순히 '이름[key] : 값[value]** 형태의 프로퍼티들을 저장하는 컨테이너이다.



기본 타입은 하나의 값만을 가지고 참조타입인 객체는 여러 개의 **프로퍼티**들을 포함할 수 있다.

객체의 프로퍼티는 기본 타입의 값을 포함하거나 다른 객체를 가르킬 수도 있다.

객체의 프로퍼티는 함수로 포함할 수 있으며, 이러한 프로퍼티를 메서드라고 한다.



**프로퍼티** - **접근 가능한 이름과 활용 가능한 값을 가지는 특별한 형태**

**메서드** - **동작을 수행하기 위해서 객체의 정보를 담고있는 프로퍼티를 사용**

~~~~javascript
// 프로퍼티
var foo={}; // 객체 생성
foo.a=2; // 연산자를 이용하여 a 라는 이름의 프로퍼티를 생성하면서 2이라는 값을 할당
var sum = foo.a+8; // 연산자를 이용하여 foo 객체의 a 프로퍼티에 접근하여 값을 활용가능하다.
console.log(sum);
> 10

//메서드
var foo={};
foo.a=2;
foo.b=3;
foo.sum=function() {console.log(foo.a+foo.b);};
foo.sum();
> 5
~~~~



## 객체 생성

객체를 생성하는 방법 3가지 방법이 있다.

1. 기본 제공 Object() 객체를 이용하는 방법
2. 객체 리터럴
3. 생산자(constructor) 함수

~~~javascript
//1. Object() 생산자 함수
//내장 Object() 생성자 함수를 이용하여 객체 생성

//빈 객체 생성
var obj = new Object();

//객체 프로퍼티 생성
obj.name = "Creatijin";
obj.age = "28";

console.log(typeof obj) // 출력값 - object
console.log(obj)  // 출력값 - { name: "Creatijin", age: "28" }
~~~

~~~javascript
//2. 리터럴 방식
//객체 리터럴 방식은 간단한 표기법으로 객체를 생성할 수 있다.

//객체 생성
var obj = {
    name: "Creatijin",
    age: "28"
}

console.log(typeof obj) // 출력값 - object
console.log(obj)  // 출력값 - { name: "Creatijin", age: "28" }
~~~

~~~javascript
//3. 생성자 함수
// 생성자 와 new 

//함수생성
function person(name) {
    this.name = name;
    //메소드 생성
	this.inroduce = function() {
		return 'My name is ' + this.name;
	}
}

// 생성자 
var c1 = new person("creatijin");
var c2 = new person("seungdols");

console.log(c1.inroduce()) // 출력값 - My name is creatijin
console.log(c2.inroduce()) // 출력값 - My name is seungdols

//생성자 함수의 장점은 초기화(initialize)를 통해 코드의 재사용성을 높인다.
~~~

