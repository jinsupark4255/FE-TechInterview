# async/await

## 비동기 처리 방식

- 자바스크립트는 싱글 스레드 프로그래밍 언어이기 때문에 비동기 처리가 기반이다.
- 비동기 처리는 결과 반환 시기를 알 수 없기에 동기적으로 처리하는 기법이 사용되어야 한다.
- async/await 방식이 있고 Promise 방식이 있다.

## Promise 방식

- 비동기 연산의 최종 완료와 그 결과값을 나타낸다.
- Promise는 세 가지 상태를 가진다.
  ```
  Pending (대기 중) : 아직 연산이 완료되지 않은 상태
  Fulfilled (이행됨) : 연산이 성공적으로 완료된 상태
  Rejected (거부됨) : 연산이 실패한 상태
  ```
- Promise를 사용하면 비동기 작업의 결과를 체인 형태로 연결할 수 있으며, 'then', 'catch' 메소드를 사용하여 성공, 실패, 완료 시 수행할 작업을 지정할 수 있다.
  ```tsx
  fetchExample()
    .then((result) => fetchExample2(result))
    .then((newResult) => fetchExample3(newResult))
    .catch((error) => console.error(error));
  ```
- Promise의 .then과 .catch는 콜백 함수를 인자로 받으며, .then의 콜백 함수의 인자에 resolve 결과 값을 넘겨주며 .catch의 콜백 함수의 인자에 reject 결과 값을 넘겨준다.
  ```tsx
  fetch('https://example.com/posts')
    .then(function(response){ //이름 없는 콜백함수와, 그 인자로 resolve 결과값인 response 넘겨줌
      response.json().then(function(data){ //response.json()이 Promise를 또 반환
        console.log('data', data);
      });
    });
    .catch(function(reason){
      console.log('reason',reason);
    });
  ```
- 또한 .then의 인자인 콜백함수가 Promise를 반환하지 않더라도 .then과 .catch는 그 결과를 Promise로 반환하기 때문에 .then 다음에 .then으로 계속 처리가 가능하다.
  ```tsx
  function handleResponse(response) {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return 'hello'; // 일반 문자열 반환
  }  

  fetch('https://example.com/data')
    .then(handleResponse) // handleResponse에서 'hello'를 반환
    .then(data => {
      console.log('Received data:', data); // 'Received data: hello' 출력
    })
    .catch(error => {
      console.error('Failed to fetch:', error);
    });
  ```

## async/await 방식

- 비동기 코드를 동기 코드처럼 보이게 하고 Promise 보다 작성하기 쉽게 만들어준다.
- async 함수는 항상 Promise를 반환하며, 함수 내부에서 await 키워드를 사용하여 Promise의 해결을 기다릴 수 있다.
  ```js
  async function asyncFunction() {
    try {
      const result = await fetchExample();
      const newResult = await fetchExample2(result);
      const finalResult = await fetchExample3(newResult);
      console.log(`Got the final result: ${finalResult}`);
    } catch (error) {
      console.error(error);
    }
  }
  ```

## Promise와 async,await의 차이점

### 가독성

- async/await을 사용하면 비동기 코드를 거의 동기 코드처럼 작성할 수 있어 가독성이 향상된다. 반면 Promise 체인은 여러개의 .then() 호출로 인해 콜백 지옥같은 thenable 지옥에 빠질 수 있으며, 복잡한 로직에서는 코드 이해가 어려울 수 있다.

### 오류 처리

- async/await는 전통적인 try-catch 문을 사용하여 오류를 처리할 수 있어, 개발자에게 친숙하다. 반면 Promise는 오류를 .catch() 메소드로 처리한다.

### 중간 값 사용

- async/await를 사용하면 각 단계에서 생성된 값에 쉽게 접근할 수 있어, 중간 결과를 재사용하기가 더 편리하다.
