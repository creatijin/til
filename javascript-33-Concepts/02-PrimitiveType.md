# Javascript 33 concepts

##Primitive Type

"Primitive" 라는 단어는 원시적인, 기초적인 이라는 뜻이다.

기초적인 타입을 말하는 것이다.

자바스크립트에서는 5가지 (숫자,문자열,블린값,null,undefined) 기본 타입이 존재한다

5가지의 특징을 알아보자.

~~~javascript
//숫자 (Number)
19920124
1992.0124

Math.pow(92, "string")  // NaN (Not a Number)

/*
숫자의 경우 정수, 소수 둘다 Number Type이며 
NaN의 경우 결과값이 숫자가 아닐때 NaN값을 출력한다.
*/

//문자열 (String)
"hello"
'creatijin'

//(1)
"hello my name is "creatijin""
//출력값 - 에러

//(2)
"hello my name is \"creatijin\""
//출력값 - hello my name is "creatijin"

/*
"",'' 둘다 String Type이며 "' ,'" 등 짝에 안맞게 사용시에는 에러를 발생한다.
(1)의 경우 "creatijin"이 부분을 자바스크립트는 변수명으로 인식한다.
(2)의 경우 \" 형식으로 넣고 출력할 경우 "creatijin"으로 포함돼서 출력한다.
*/

//블린값 (Boolean)
true
false
"true"
"false"

/*
블린값은 true,false로 참,거짓으로 나뉘며 "",''안에 쓸 경우 string으로 인식한다.
*/

//null
//undefined

/*
null과 undefined는 존재하지 않음으로 정의가 됨, 정의가 되지 않음 으로 나뉜다.
*/
let hello;
hello
//undefined
console.log(hello === undefined);
//true
console.log(hello === null);
//false

hello = null;
hello
//null
/*
undefined는 정의되지 않은 상태이고
null의 경우 "존재하지 않음" 이라는 값(valie)를 가지게 된다.
이 둘의 차이는 엄연히 다르다.
*/
~~~

**ES6에 추가된 symbol의 경우 추후에 업데이트 예정**