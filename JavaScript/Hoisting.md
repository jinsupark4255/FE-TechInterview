# Hoisting
자바스크립트에서 Hoisting은 변수나 함수 선언이 그들이 포함된 스코프의 최상단으로 끌어올려진 것처럼 동작하는 특성을 말한다.

## Hoisting의 동작 방식
### 변수 호이스팅
- 'var' 키워드로 선언된 변수는 호이스팅되어 스코프의 최상단으로 끌어올려진다. 단, 변수를 선언만 하고 초기화하지 않은 경우에는 기본적으로 'undefined'로 설정된다.
- 'let'과 'const'로 선언된 변수도 호이스팅되지만, 선언된 위치에서 초기화가 이뤄진다. 실제 코드에서 선언문에 도달하기 전에 해당 변수를 사용하려고 하면 'Reference' 에러가 발생한다.
```js
console.log(myVar); // undefined
var myVar = 5;
console.log(myVar); // 5
```

```js
console.log(myLet); // ReferenceError: Cannot access 'myLet' before initialization
let myLet = 10;
console.log(myLet); // 10
```

### 함수 호이스팅
- 함수 선언문(function)은 전체 선언이 호이스팅되며, 이는 함수를 선언하기 전 어디서든 호출할 수 있음을 의미한다.
- 함수 표현식은 해당 표현식이 변수에 할당되는 방식에 따라 호이스팅의 영향을 받는다.
```js
console.log(myFunc);  // undefined
myFunc();             // TypeError: myFunc is not a function

var myFunc = function() {
  console.log("Hello");
};

myFunc();             // Hello

```

### 정리
호이스팅은 때로 코드의 가독성과 실행 흐름을 혼란스럽게 만들 수 있으므로, var 대신 let이나 const를 사용하고, 함수 표현식 대신 함수 선언문을 사용하는 것이 좋습니다.
