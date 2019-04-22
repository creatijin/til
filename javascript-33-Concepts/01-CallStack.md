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



### 요약

리스트가 존재하고 함수는 리스트에 추가가 된다.

실행이 완료되면 함수는 리스트에서 제거 된다.