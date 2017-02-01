# Stack

## 설명

스택은 LIFO(Last In First Out)의 원리에 따라 정렬된 컬렉션이다. 스택에서 종단점은 꼭대기와 바닥 둘 뿐인데 가장 최근 자료는 꼭대기 근처에, 가장 오래된 자료는 바닥 근처에 위치해서 가장 마지막에 들어온 자료가 가장 먼저 나가게 된다.

## 구현

``` javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(element) {
    this.items.push(element);
  }

  pop() {
    return this.items.pop();
  }

  peek() {
    return this.items[this.items.length - 1];
  }

  size() {
    return this.items.length;
  }

  clear() {
    this.items = [];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  print() {
    console.log(this.items.toString());
  }
}
```

## 예제

``` javascript
// 10진수를 다른 진수로 변환
function convertBase(decNum, base) {
  let stack = new Stack(),
      result = '',
      digits = '0123456789ABCDEF';

  while (decNum > 0) {
    let mod = decNum % base;
    stack.push(mod);
    decNum = Math.floor(decNum / base);
  }

  while (!stack.isEmpty()) {
    result += digits[stack.pop()];
  }

  return result;
}
```