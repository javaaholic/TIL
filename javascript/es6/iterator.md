# Iterator

## Iteration Protocol

루프, 생성자가 어떤 객체의 값들을 순회하기 위한 인터페이스 구현 규칙으로 ES6는 Iterable Protocol과 Iterator Protocol 두 가지로 나누어 규정한다.

## Iterator Protocol

Iterator 객체는 Iterator Protocol을 따르는 객체로 그 다음 요소를 반환하는 next() 메소드를 구현한다.

## Iterable Protocol

Iterable은 Iterable Protocol을 구현한 객체로 Symbol.iterator을 property key로 갖고 있으며 Iterator 메소드는 Iterator 객체를 반환한다.

## Generator

이 함수를 호출하면 generator 객체(iterable, iterator protocol을 모두 구현한 객체)를 반환한다.

``` javascript
function* generator1() {
  yield 1;
  yield 2;
  yield 3;
}

let gen1 = generator1();   
console.log(gen1.next()); // Object {value: 1, done: false}
console.log(gen1.next()); // Object {value: 2, done: false} 
console.log(gen1.next()); // Object {value: 3, done: false} 
console.log(gen1.next()); // Object {value: undefined, done: true}

function* generator2() {
  yield* generator1();
  yield* [4, 5];
}

let gen2 = generator2();
console.log(gen2.next()); // Object {value: 1, done: false}
console.log(gen2.next()); // Object {value: 2, done: false}
console.log(gen2.next()); // Object {value: 3, done: false}
console.log(gen2.next()); // Object {value: 4, done: false}
console.log(gen2.next()); // Object {value: 5, done: false}
console.log(gen2.next()); // Object {value: undefined, done: true}
```

## for...of Loop

iterable 객체 값을 순회한다.

``` javascript
function* generator() {
  yield* [1, 2, 3, 4, 5];
}

for (let i of generator()) {
  console.log(i); // 1, 2, 3, 4, 5 출력
}
```