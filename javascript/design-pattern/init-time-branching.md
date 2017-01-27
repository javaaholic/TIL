# Init-Time Branching

## 설명

초기화 단계에서 분기하여 같은 함수를 환경에 따라 다르게 정의하는 패턴이다. 주요 기능에 대한 호환성을 보장할 때 사용하기 좋은 패턴이다. 예) 이벤트 핸들러, XMLHttpRequest등

## 구현

``` javascript
let getXHR = (() => {
  if (window.XMLHttpRequest) {
    return function () {
      return new XMLHttpRequest();
    }
  }
  try {
    let xhr = new ActiveXObject('MSXML2.XMLHTTP.6.0');
    return function () {
      return new ActiveXObject('MSXML2.XMLHTTP.6.0');
    }
  } catch (e) {
    try {
      let xhr = new ActiveXObject('MSXML2.XMLHTTP.3.0');
      return function () {
        return new ActiveXObject('MSXML2.XMLHTTP.3.0');
      }
    } catch (e) {
      alert('이 브라우저는 XMLHttpRequest를 지원하지 않습니다.');
    }
  }
})();
```

## 주의할 점

최초 초기화 때 컴퓨팅 자원 소모가 있다.