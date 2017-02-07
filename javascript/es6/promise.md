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

![promise](./promises.png "출처: MDN")

## Promise.prototype.then(onFulfilled, onRejected)

이행되거나 거부된 후의 처리를 한다. onFulfilled, onRejected 2개의 콜백을 갖으며 이행된 경우에는 onFulfilled 콜백을, 거부된 경우에는 onRejected 콜백을 호출한다. onRejected 콜백은 executor 스코프에서 예외가 발생해도 호출된다. 콜백의 반환값으로 resolve되는 promise 객체 또는 새 promise 객체를 반환한다.

``` javascript
let promise = new Promise(function (resolve, reject) {
  console.log('==== async start ====');
  setTimeout(function () {
    resolve('Hello');
  }, Math.floor(Math.random() * 3000));
});

promise.then(function (value) {
  console.log(`${value}, World!`);
  return new Promise(function (resolve, reject) {
    setTimeout(function () {
      resolve('Bye');
    }, Math.floor(Math.random() * 3000));
  });
}).then(function (value) {
  console.log(`${value}, World!`);
}).then(function () {
  console.log('==== async end ====');
});

console.log('I am a sync code!');
```

## Promise.prototype.catch(onRejected)

예외만 처리하고 싶을 때 사용한다. 마찬가지로 반환값으로 resolve되는 promise 객체 또는 새 promise 객체를 반환한다.

``` javascript
new Promise(function (resolve, reject) {
  let randNum = Math.floor(Math.random() * 10);
  console.log(`${randNum} selected`);
  if (randNum < 3) {
    reject('low number');
  } else {
    resolve(randNum);
  }
}).then(function (value) {
  if (value > 6) {
    throw 'high number';
  }
  console.log(`success! - ${value}`);  
}, function (reason) {
  console.log(`error1 msg: ${reason}`);
}).catch(function (reason) {
  console.log(`error2 msg: ${reason}`);
});
```

## Promise.resolve(value)

## Promise.reject(reason)

## Promise.all(iterable)

주어진 iterable 객체가 모두 이행될 때 resolved promise 객체를 반환하는 메소드이다.

``` javascript
var promise1 = new Promise(function (resolve, reject) {
  setTimeout(function () {
    console.log('promise1 call');
    resolve();
  }, 2000);
});

var promise2 = new Promise(function (resolve, reject) {
  setTimeout(function () {
    console.log('promise2 call');
    resolve();
  }, 3000);
});

Promise.all([promise1, promise2]).then(function () {
  console.log('complete'); // 3초 후에 출력
});
```

## Promise.race(iterable)

주어진 iterable 객체중 하나라도 이행될 떄 해당 resolved promise 객체를 반환하는 메소드이다.

``` javascript
var promise1 = new Promise(function (resolve, reject) {
  setTimeout(function () {
    resolve('promise1 call');
  }, 2000);
});

var promise2 = new Promise(function (resolve, reject) {
  setTimeout(function () {
    resolve('promise2 call');
  }, Math.random() * 4000);
});

Promise.race([promise1, promise2]).then(function (value) {
  console.log(value);
});
```