# Callback

## 설명

변수나 인자로 넘긴 함수를 필요할 때 호출하는 패턴이다.

## 구현

``` javascript
function ajax(method, url, data, callback) {
  var xhr = new XMLHttpRequest();
  xhr.open(method, url);

  xhr.onload = function () {
    if (xhr.status === 200) {
      callback.call(this, xhr.responseText);
    }
  }
  
  xhr.send(data);
}

ajax('post', '/articles', article, function (responseText) {
  if (responseText === 'success') {
    console.log('글이 작성되었습니다.');
    ajax('get', '/articles/' + article.id, null, readArticle);
  } else {
    console.log('글 작성에 실패했습니다.');
  }
});
  
function readArticle(responseText) {
  console.log(responseText);
}
```

## 주의할 점

콜백이 너무 반복되면 가독성이 떨어지므로 적당히 함수명으로 분리하는 것이 필요하다.