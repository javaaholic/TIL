# Self-Defining Function

## 무엇인가?

자신을 다시 정의하는 함수 패턴이다.

## 구현

``` javascript
let defineFunc = function () {
  let data = getData();

  defineFunc = function () {
    console.log(data);
  }

  defineFunc();
}
```