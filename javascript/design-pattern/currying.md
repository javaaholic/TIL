# Currying

## 무엇인가?

일부 인자만 먼저 입력해두고 나머지만 입력받을 수 있도록 새로운 함수를 만드는 패턴이다.

## 구현

``` javascript
Function.prototype.curry = function () {
  if (arguments.length < 1) {
    return this;
  }
  var _this = this,
    args = Array.from(arguments);

  return function () {
    return _this.apply(this, args.concat(Array.from(arguments)));
  }
}

function unitConvert(fromUnit, toUnit, factor, input) {
  console.log(`${factor * input}${toUnit}`);
}

var cmToM = unitConvert.curry('cm', 'm', 0.01),
  mToKm = unitConvert.curry('m', 'km', 0.001);

console.log(cmToM(100)); // 1m
console.log(mToKm(1));   // 0.001km
```

## 주의할 점

프로그램이 돌아가는 순서를 파악하기 어려울 수 있어 개발 효율성과 소스 관리에 대한 균형이 필요하다.