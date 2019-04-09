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



### 객체 프로퍼티 읽기/쓰기/갱신

- 대괄호 ([]) 표기법
- 마침표 (.) 표기법

~~~javascript
//객체 리터럴로 생성
var obj = {
    name: "Creatijin",
    age: "28",
    coffee: "KANU"
}

//읽기
console.log(obj.name);	// 출력값 - Creatijin
console.log(obj['name']);	// 출력값 - Creatijin

//갱신
obj.coffee = "Maxim";
console.log(obj.coffee);	//출력값 - Maxim
console.log(obj["coffee"]);	//출력값 - Maxim


//동적 생성
obj.apple = "mac";
console.log(obj.apple);	// 출력값 - mac
~~~



#### for in 문 과 삭제

for in 문을 사용하면 객체에 포함된 모든 프로퍼티에 대한 루프를 수행 가능하다.

~~~javascript
var obj = {
    name: "Creatijin",
    age: "28",
    coffee: "KANU"
}

var prop;
for (prop in obj) {
    console.log(prop, obj.prop)
}

// 출력값
name Creatijin
age 28
coffee KANU

delete obj.coffee;
console.log(obj.coffee);	// 출력값 - undefined
~~~



####객체 프로퍼티 삭제

**delete** 연산자를 이용하면 객체의 프로퍼티를 즉시 삭제할 수 있다.

**delete 연산자는 객체의 프로퍼티를 삭제할 뿐 객체 자체는 삭제가 불가능하다.**

~~~javascript
var obj = {
    name: "Creatijin",
    age: "28",
    coffee: "KANU"
}

console.log(obj.coffee); // 출력값 - KANU
delete obj.coffee; // 출력값 coffee 프로퍼티 삭제
console.log(obj.coffee); // 출력값 - undefind

delete obj;
console.log(obj.name); // 출력값 - Creatijin
~~~



### 참조 타입 특성

자바스크립트에서 기본타입을 제외한 모든 값은 객체이고 이것을 **참조타입**이라고 부른다.

객체의 모든 연산이 실제 값이 아닌 참조 값으로 처리된다.

~~~javascript
var A = { val : 40 } // (1)
var B = A; // (2)

console.log(A.val);	// 출력값 - 40
console.log(B.val);	// 출력값 - 40

B.val = 50; // (3)

console.log(A.val);	// 출력값 - 50
console.log(B.val);	// 출력값 - 50
~~~

1. A 변수에 40을 참조값으로 저장한다.
2. B 변수에 A 변수 값을 할당한다. B, A는 같은 참조값을 바라보게 된다.
3. B 변수의 val의 값을 50으로 갱신했다. 이때 같은 참조값을 바라보는 A.val도 50의 값으로 변경된다.



#### 객체 비교

동등 연산자를 사용할때 객체의 프로퍼티 값을 비교하는 것이 아닌 참조값을 비교한다.

~~~javascript
var a = 100;
var b = 100;

var objA = { val: 100 };
var objB = { val: 100 };
var objC = objB;

console.log(a == b)	// 출력값 - true (1)
console.log(objA == objB)	// 출력값 - false (2)
console.log(objB == objC)	// 출력값 - true (2)
~~~