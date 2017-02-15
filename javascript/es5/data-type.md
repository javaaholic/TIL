# 데이터 타입
ES5에서 데이터 타입은 number, string, boolean, undefined, null로 이루어진 기본(원시) 데이터 타입과 참조 타입 object가 있다. ES6에는 기본 데이터 타입에 symbol이 추가된다.

## typeof 연산자
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

## undefined 타입
초기화되지 않고 선언된 변수는 undefined가 할당된다. 아예 선언하지 않은 변수를 참조하려고 하면 ReferenceError가 발생하는데 이 변수를 typeof로 확인하면 이 때도 문자열 undefined가 반환된다.

``` javascript
var num;
console.log(num === undefined);          // true
console.log(typeof str === 'undefined'); // true
console.log(str);                        // Uncaught ReferenceError
```

## null 타입
null 타입은 특별한 값 null을 가지며, null은 빈 객체를 가리키는 포인터이다. 객체를 가리킬 변수라면 null로 초기화 하자. undefined와 == 비교시 true를 반환한다.

## boolean 타입
true, false 2가지 리터럴 값을 갖는다. Boolean 함수를 이용해서 boolean 타입으로 변환할 수 있다. if문 같은 제어문은 자동으로 타입을 boolean으로 바꾼다. 다음과 같은 규칙으로 변환한다.

| type      | true                    | false     |
|-----------|-------------------------|-----------|
| boolean   | true                    | false     |
| string    | ''을 제외한 모든 문자열   | ''        |
| number    | 0, NaN을 제외한 모든 숫자 | 0, NaN    |
| object    | null을 제외한 모든 객체   | null      |
| undefined | 없음                     | undefined |

## number 타입
정수와 부동소수점 숫자를 나타낸다. 부동소수점 숫자를 나타낼 때는 정수를 저장할 떄에 비해 메모리를 2배 소모한다. 부동소수점 숫자를 표현할 때 'e-표기법'을 사용할 수 있다.

``` javascript
// IEEE-754에서 정의한 방식대로 부동소수점 숫자를 계산하기 떄문에 다음과 같은 결과가 나온다.
console.log(0.1 + 0.2); // 0.30000000000000004
```

### NaN
Not A Number로 숫자를 반환할 것으로 의도한 조작이 실패했을때 에러 대신 반환하는 값이다. isNaN()으로 검사한다.

``` javascript
// NaN끼리도 일치하지 않는다.
console.log(NaN == NaN); // false
```

### 슷자 변환
Number, parseInt, parseFloat 함수를 이용해서 다른 타입을 number 타입으로 변환할 수 있다. parseInt, parseFloat 함수가 더 일관되게 작동한다. 단항 덧셈 연산자(+)는 Number() 함수와 같은 일을 한다.

## string 타입
16비트 유니코드 문자의 연속으로 된 문자열이다.

### 문자열 변환
toString 메소드를 이용해서 문자열로 변환할 수 있다. null이나 undefined는 String 함수를 이용해서 문자열로 변환할 수 있다.

## object 타입
ECMAScript에서 객체는 데이터와 기능의 집합이다.

ECMAScript의 Object 타입은 자바의 java.lang.Object처럼 이 타입에서 파생되는 모든 객체의 원형으로 Object 타입의 인스턴스는 Object 타입의 프로퍼티와 메서드를 전부 상속한다.

Object의 인스턴스는 다음 프로퍼티와 메서드를 가진다.
- constructor - 해당 객체를 만드는데 쓰인 함수
- hasOwnProperty(propertyName) - 해당 프로퍼티가 객체 인스턴스에 고유하며 프로토타입에서 상속하지 않았음을 확인한다.
- isProtoTypeOf(object) - 해당 객체가 다른 객체의 프로토타입인지 확인한다.

ECMAScript에서는 모든 객체가 Object에 기반해 만들어지므로 이들 프로퍼티와 메서드는 모든 객체에 존재한다.