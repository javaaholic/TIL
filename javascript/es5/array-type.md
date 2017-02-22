# Array 타입

## 배열 감지

``` javascript
var arr = [];

console.log(arr instanceof Array); // true
console.log(Array.isArray(arr));   // true
```

## 변환 메서드

``` javascript
var colors = ['red', 'blue', 'green'];

// 내부적으로 toString()을 호출한다.
console.log(colors.toString()); // red,blue,green

// join 메서드를 사용하면 다른 구분자를 써서 문자열로 나타낼 수 있다.
console.log(colors.join('||')); // red||blue||green
```

## 스택 메서드
배열은 push() 메서드와 pop() 메서드를 이용해서 스택처럼 동작할 수 있다.

``` javascript
var colors = ['red', 'blue', 'green'];

console.log(colors.push('yellow')); // 4
console.log(colors);                // ["red", "blue", "green", "yellow"]
console.log(colors.pop());          // yellow
console.log(colors.length);         // 3
```

## 큐 메서드
shift() 메서드와 push() 메서드를 이용해서 큐를 구현할 수 있다.

``` javascript
var animals = [];

console.log(animals.push('dog')); // 1
console.log(animals.push('cat')); // 2
console.log(animals);             // ["dog", "cat"]
console.log(animals.shift());     // dog
console.log(animals);             // ["cat"] 

// unshift() 메서드를 사용하면 앞에서 추가할 수 있다.
console.log(animals.unshift('tiget')); // 2
console.log(animals.unshift('lion'));  // 3
console.log(animals);                  // ["lion", "tiget", "cat"]
```

## 정렬 메서드
순서를 뒤집는 reverse()와 비교 함수를 넘길 수 있는 sort()가 있다.

``` javascript
var numbers = [1, 2, 3, 100];

// reverse()
console.log(numbers.reverse()); // [100, 3, 2, 1]

// sort() 비교 함수를 넘기지 않으면 문자열 비교를 한다.
console.log(numbers.sort()); // [1, 100, 2, 3]

// sort(compareFn) 비교 함수의 반환값이 0보다 크면 순서를 바꾸고 아니면 그대로 둔다.
console.log(numbers.sort(function (num1, num2) { return num1 - num2; })); // [1, 2, 3, 100]
```

## 조작 메서드
- concat: 현재 배열을 복사한 다음 메서드의 매개변수를 새 배열 마지막에 추가해서 반환한다.
- slice: 배열에 포함된 데이터 일부를 가진 새 배열을 반환한다.
- splice: 삭제, 삽입, 대체할 수 있다.

``` javascript
var numbers = [1, 2, 3];

// concat(...items)
console.log(numbers.concat());          // [1, 2, 3]
console.log(numbers.concat([4, 5, 6])); // [1, 2, 3, 4, 5, 6]
console.log(numbers.concat(4));         // [1, 2, 3, 4]

// slice(start?, end?) 
// 매개 변수로 음수를 넘기면 length를 더한 값을 대신 사용한다.
console.log(numbers.slice());       // [1, 2, 3]
console.log(numbers.slice(1));      // [2, 3]
console.log(numbers.slice(1, 2));   // [2]
console.log(numbers.slice(-2, -1)); // [2] 

// splice(start, deleteCount?) 삭제
var numbers = [1, 2, 3, 4, 5];
console.log(numbers.splice(3)); // [4, 5]
console.log(numbers);           // [1, 2, 3]

var numbers = [1, 2, 3, 4, 5];
console.log(numbers.splice(1, 3)); // [2, 3, 4]
console.log(numbers);              // [1, 5]

// splice(start, deleteCount, ...items) 삽입, 대체
var numbers = [1, 2, 5];
numbers.splice(2, 0, 3, 4);
console.log(numbers); // [1, 2, 3, 4, 5]

var numbers = [1, 2, 100, 4, 5];
numbers.splice(2, 1, 3);
console.log(numbers); // [1, 2, 3, 4, 5]
``` 

## 위치 메서드

``` javascript
var arr = ['a', 'b', 'c', 'b', 'a'];

// indexOf(searchElement, fromIndex?)
console.log(arr.indexOf('b'));    // 1
console.log(arr.indexOf('b', 2)); // 3

// lastIndexOf(searchElement, fromIndex?)
console.log(arr.lastIndexOf('b'));    // 3
console.log(arr.lastIndexOf('b', 2)); // 1

// 찾지 못하면 -1을 반환
console.log(arr.indexOf('d')); // -1
```

## 반복 메서드

## 감소 메서드