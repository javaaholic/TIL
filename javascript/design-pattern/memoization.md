# Memoization

## 설명

패턴의 이름대로 함수 또는 객체에 메모를 하여 캐시를 사용하는 것처럼 활용할 수 있다. 컴퓨팅 자원을 사용하거나 처리 시간이 긴 산술식 또는 서버에 동일한 요청을 보내는 경우 사용하면 좋다.

## 구현

``` javascript
Function.prototype.memoize = function () {
  let _this = this, memo = {};

  return function (prop) {
    let argsString = JSON.stringify(arguments);
    
    if (memo.hasOwnProperty(argsString)) {
      return memo[argsString];
    }

    let returnValue = _this.apply(this, arguments);
    memo[argsString] = returnValue;
    return returnValue;
  }
}
```

## 주의할 점

Function.prototype에 추가하는 방식은 산술처리나 XMLHttpRequest에 사용하면 좋고 재귀함수는 직접 Memoization 패턴을 설계하여 사용하는 것이 성능에 좋다.