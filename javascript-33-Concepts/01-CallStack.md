# Javascript 33 concepts

## Call Stack

Call stack은 자바스크립트가 함수를 실행하는데 핸들링 하는 방법 중 하나이다.

자바스크립트가 실행해야하는 함수를 스택(stack) 위에 올린다.

여기서 스택을 쌓아올리는 모습은 책을 쌓아 올리는 형태이다.

~~~javascript
function three(){
    console.log("javascript call stack")
}
function two(){
    three();
}
function one(){
    two();
}
function zero(){
    one();
    throw Error("omg error");
}
zero();

// 출력물
// "javascript call stack"
// Uncaight Error: omg error

~~~

위 코드를 살펴보면 zero(); 함수를 실행하고 zero 안에 one 그 다음 one 안에 two 순서로 실행이 된다.

그러면 Call Stack 은 zero()가 가장 밑 그다음 one,two,three순으로 쌓이게 되고 그다음 각 함수가 끝나면

Three, two, one, zero 순서로 종료된다. 여기서 one() 다음 throw Error는 one()의 실행이 끝난다음 순서로 진행된다.



#### +스택붕괴

자바스크립트에서는 스택을 무한으로 쌓을 수 있는게 아니기 때문에 스택이 붕괴될때 에러가 나는 현상이 있다.

~~~javascript
function hello() {
    bye();
}
function bye() {
    hello();
}
bye();

//출력값
/*
VM83:4 Uncaught RangeError: Maximum call stack size exceeded
    at bye (<anonymous>:4:13)
    at hello (<anonymous>:2:5)
    at bye (<anonymous>:5:5)
    at hello (<anonymous>:2:5)
    at bye (<anonymous>:5:5)
    at hello (<anonymous>:2:5)
    at bye (<anonymous>:5:5)
    at hello (<anonymous>:2:5)
    at bye (<anonymous>:5:5)
    at hello (<anonymous>:2:5)
*/
~~~

위에 예제를 보듯 "Maximum call stack exceeded" 라는 문구가 뜨면서 에러가 발생한다.

자바스크립트는 스택에 올릴 수 있는 수가 제한이 있다.



### 요약

리스트가 존재하고 함수는 리스트에 추가가 된다.

실행이 완료되면 함수는 리스트에서 제거 된다.