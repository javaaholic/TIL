# Basics

## let

블록 스코프 변수를 선언하는 키워드이다.

## const

값을 다시 할당할 수 없는 상수를 할당한다. 블록 스코프 변수이다.

## default parameter

``` javascript
function sum(x = 1, y = 2, z = 3) {
  return x + y + z;
}

sum(100); // 105
```

## spread operator

이터러블 객체를 개별 값으로 펼친다. sperad operator는 "..."으로 표시한다.

``` javascript
// 함수 인자로 넘기기
function sum(a, b, c) {
  return a + b + c;
}

let arr1 = [1, 2, 3];

console.log(sum(...arr1)); // 6

// 다른 배열의 일부로 만들기
let arr2 = [...arr1, 4, 5, 6];

console.log(arr2); // [1, 2, 3, 4, 5, 6]

// 다른 배열로 밀어넣기
let arr3 = [7, 8, 9];

arr2.push(...arr3);

console.log(arr2); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## rest parameter

rest parameter는 함수의 마지막 파라미터 앞에 "..."을 붙여 사용한다. 함수의 가변인자의 개수를 포착하는데 사용된다.

``` javascript
function print(...arr) {
  console.log(arr);
}

print(1, 2, 3, 4); // [1, 2, 3, 4]
```