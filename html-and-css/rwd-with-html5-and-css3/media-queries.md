# 미디어 쿼리
미디어 쿼리는 디바이스의 특징에 따라 특정 CSS 스타일을 적용할 수 있도록 해준다. 예를 들면 뷰포트의 폭, 화면 비율, 방향등에 따라 콘텐츠가 표시되는 방법을 변경할 수 있다.

## 미디어 쿼리 사용하기

``` html
<!-- screen에서 400px이상 -->
<link rel="stylesheet" href="css/style.css" media="screen and (min-width: 400px)">

<!-- print에서 600px이하 -->
<link rel="stylesheet" href="css/style.css" media="print and (max-width: 600px)">

<!-- all에서 400px이상 600px이하 -->
<link rel="stylesheet" href="css/style.css" media="all and (min-width: 400px) and (max-width: 600px)">

<!-- all은 생략 가능 -->
<link rel="stylesheet" href="css/style.css" media="(min-width: 400px) and (max-width: 600px)">
```

``` css
/* screen에서 400px이상 */
@media screen and (min-width: 400px) {}

/* print에서 600px 이하 */
@media print and (max-width: 600px) {}

/* all에서 400px이상 600px이하 */
@media all and (min-width: 400px) and (max-width: 600px) {}

/* all은 생략 가능 */
@media (min-width: 400px) and (max-width: 600px) {}
```

@import로도 사용할 수 있지만 HTTP의 요청이 증가하기 떄문에 성능상 권장되지 않는다.

## 미디어 쿼리 고려사항
link 태그를 통해 각각의 미디어 쿼리를 분할하면 HTTP 요청이 늘어나서 성능상 악영향을 줄 수 있다. 

## viewport