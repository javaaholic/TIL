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

rest parameter는 함수의 마지막 파라미터 앞에 "..."을 붙여 사용한다. 함수의 가변인자 개수를 알지 못할 때 사용한다.

``` javascript
function print(...arr) {
  console.log(arr);
}

print(1, 2, 3, 4); // [1, 2, 3, 4]
```

## destructuring

destructuring assignment는 이터러블이나 객체의 프로퍼티를 배열이나 객체 생성자 리터럴과 비슷한 구문으로 변수에 할당하는 표현식이다.

### array destructuring

이터러블 객체에서 값을 추출하여 변수에 할당한다.

``` javascript
let [a, b, c] = [1, 2, 3];
console.log(a, b, c); // 1 2 3

// rest operator를 사용할 수 있다.
let [d, ...e] = [4, 5, 6, 7];
console.log(d, e); // 4 [5, 6, 7]

// 변수의 기본값을 지정할 수 있다.
let [f, g = 100] = [];
console.log(f, g); // undefined 100

// 중첩 배열 해체
let [h, [i, j]] = [[10], [11, 12]];
console.log(h, i, j); // [10] 11 12

// 파라미터로 배열 해체 할당 사용
function printArr([a, b, c = 999]) {
  console.log(a, b, c);
}

printArr([100, 101]); // 100 101 999
```

### object destructuring

객체 프로퍼티 값을 추출해서 변수에 할당한다.

``` javascript
let {a, b} = { a: 1, b: 2 };
console.log(a, b); // 1 2

let { a: name, b: say } = { a: 'jin', b: 'hello' };
console.log(name, say); // jin hello

let { name, info: { sex: gender, age } } = { name: 'jin', info: { sex: '남', age: 27 } };
console.log(name, gender, age); // jin 남 27

function printObj({a, b, c = 100}) {
  console.log(a, b, c);
}

printObj({ a: 1, b: 2 }); // 1 2 100
```

## Arrow Function

=> 연산자로 익명함수를 생성한다.

### 화살표 함수에서 this값

화살표 함수 내부에서 this는 둘러싼 스코프의 this값을 참조한다.

``` javascript
let obj = {
  func: function () {
    console.log(this);
    let func = () => {
      console.log(this);
    }
    func();
  }
}

obj.func(); // Object {}, Object {}
```

## 강화된 객체 리터럴

``` javascript
let name = 'jin', age = 27;
let profile = { name, age };

console.log(profile); // { name: 'jin', age: 27 }

let obj = {
  func() {
    console.log(this);
  }
}

obj.func(); // Object {}
```

## Template String

``` javascript
let name = 'Jin';
console.log(`Hello, ${name}!`); // Hello, Jin!

// multi line
console.log(`
안녕하세요!
2줄도 가능해요!
`);
```