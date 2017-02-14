# 1장 반응형 웹 디자인 핵심

## 반응형 웹 디자인이란?

1. 유연한 그리드 레이아웃<sup>Flexible Grid Layout</sup>
2. 유연한 이미지<sup>Flexible Image</sup>와 미디어
3. 미디어 쿼리<sup>Media Query</sup>

## 반응형 웹 디자인 핵심
초기에는 '데스크탑'의 고정된 폭 디자인으로 만드는 것이 일반적이었으나 반대 방향에서 시작하는 모바일 퍼스트가 더 효과적임이 알려졌다.

## 브라우저 지원 수준 결정
점진적 향상이 우아한 성능 저하보다 쉽다.

## viewport란?
브라우저에서 보이는 영역을 말한다. head에 다음 태그를 추가함으로써 기기의 가로폭에 맞게 렌더링할 수 있다.

``` html
<meta name="viewport" content="width=device-width">
```

## CSS로 유동형 이미지<sup>Fluid Image</sup> 만들기
다음을 사용하면 유동형 이미지를 만들 수 있다. width를 사용하지 않고 max-width를 사용하는 이유는 이미지의 원본 크기를 초과하지 않기 위해서이다. 

``` css
img {
  max-width: 100%;
}
```

## rem 변환
브라우저의 디폴트 폰트 사이즈는 16px이다. 따라서 px값을 16으로 나누면 rem값으로 바꿀 수 있다.