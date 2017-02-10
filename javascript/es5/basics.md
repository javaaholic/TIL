# 기초

## 데이터 타입
ES5에서 데이터 타입은 number, string, boolean, undefined, null로 이루어진 원시 데이터 타입과 참조 데이터 타입 object가 있다. ES6에는 원시 데이터 타입에 symbol이 추가된다.

### typeof 연산자
typeof 연산자를 사용해서 타입을 확인할 수 있다. null은 빈 객체를 참조하므로 object를 반환한다. function은 object이나 typeof로 확인하면 function을 반환한다.

``` javascript
console.log(typeof 1);         // number
console.log(typeof 'Hello');   // string
console.log(typeof true);      // boolean
console.log(typeof null);      // object
console.log(typeof {});        // object
console.log(typeof undefined); // undefined
console.log(typeof Function);  // function
console.log(typeof Symbol());  // symbol
```

### undefined 타입
초기화되지 않고 선언된 변수는 undefined가 할당된다. 아예 선언하지 않은 변수를 참조하려고 하면 ReferenceError가 발생하는데 이 변수를 typeof로 확인하면 이 때도 문자열 undefined가 반환된다.

``` javascript
var num;
console.log(num === undefined);          // true
console.log(typeof str === 'undefined'); // true
console.log(str);                        // Uncaught ReferenceError
```

### null 타입
null 타입은 특별한 값 null을 가지며, null은 빈 객체를 가리키는 포인터이다. 객체를 가리킬 변수라면 null로 초기화 하자. undefined와 == 비교시 true를 반환한다.

### boolean 타입
true, false 2가지 리터럴 값을 갖는다. Boolean 함수를 이용해서 boolean 타입으로 변환할 수 있다. if문 같은 제어문은 자동으로 타입을 boolean으로 바꾼다. 다음과 같은 규칙으로 변환한다.

| type      | true                    | false     |
|-----------|-------------------------|-----------|
| boolean   | true                    | false     |
| string    | ''을 제외한 모든 문자열   | ''        |
| number    | 0, NaN을 제외한 모든 숫자 | 0, NaN    |
| object    | null을 제외한 모든 객체   | null      |
| undefined | 없음                     | undefined |

### number 타입
Number, parseInt, parseFloat 함수를 이용해서 다른 타입을 number 타입으로 변환할 수 있다. parseInt, parseFloat 함수가 더 이해하기 쉽게 작동한다.

### string 타입
toString 메소드를 이용해서 문자열로 변환할 수 있다. null이나 undefined는 String 함수를 이용해서 문자열로 변환할 수 있다.