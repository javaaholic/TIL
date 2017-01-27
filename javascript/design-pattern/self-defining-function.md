# Self-Defining Function

## 설명

자신을 다시 정의하는 함수 패턴이다. 불필요한 컴퓨팅 자원 소모를 최적화 할 때 사용할 수 있다. 또 함수가 한 번만 호출되어야 하거나 ajax로 서버에 요청을 보낼 때 사용하면 유효하다.

## 구현

``` javascript
let addComment = function () {
  let divCommentWrapper = document.getElementById('comment-wrapper'),
      divComment = document.createElement('div'),
      inputComment = document.getElementById('input-comment');
      
  addComment = function () {
    divComment.innerHTML = inputComment.value;
    inputComment.value = '';
    divCommentWrapper.appendChild(divComment.cloneNode(true));
  }

  addComment();
}
```

## 주의할 점

불필요한 클로저가 생성되서 데이터가 계속 메모리에 남아 있을 수 있다.