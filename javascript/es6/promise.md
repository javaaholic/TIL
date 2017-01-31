# Promise

## 자바스크립트 실행 모델

자바스크립트 코드는 싱글 스레드로 돌아가며 콜백이나 이벤트 처리와 같은 비동기 처리를 위한 큐를 가지고 있다.

## Promise 생성자

promise 생성자의 인자로 비동기 작업에 해당하는 콜백을 넘기며 이것을 executor라고 한다. executor의 인자로 resolve, reject 콜백이 들어가며 성공하면 resolve에 결과값을, 실패하면 reject에 실패 사유를 전달한다.

``` javascript
let promise = new Promise(function (resolve, reject) {
  let xhr = new XMLHttpRequest();

  xhr.open(method, url);

  xhr.onload = function () {
    if (xhr.status === 200) {
      resolve(xhr.responseText);
    }
  }

  xhr.onerror = function () {
    reject('실패 사유');
  }

  xhr.send();
});
```

## Promise 4가지 상태

promise는 다음 4가지 상태값을 가진다.

### pending

resolve, reject 콜백 실행전 promise는 pending 상태다.

### fulfilled

resolve 콜백이 promise 객체 아닌 인자 또는 인자 없이 실행될 때 fulfilled 상태다.

### rejected

executor 스코프에서 예외가 발생하거나 reject 콜백이 실행될 경우 rejected 상태다.

### setteled

pending 상태가 아닌 fulfilled 또는 rejected 중 하나의 상태를 가지는 확정 상태다.