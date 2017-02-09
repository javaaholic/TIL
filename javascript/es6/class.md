# Class

## 설명

ES6에서 새로 추가된 구문으로 다른 언어에서처럼 class를 만들 수 있다.

## 구현

``` javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  move() {
    console.log(`${this.name} moved...`);
  }
}

class Man extends Animal {
  constructor(name) {
    super(name);
  }

  say() {
    console.log('Hello, World!');
  }
}

class Dog extends Animal {
  constructor(name) {
    super(name);
  }

  move() {
    console.log('Bow-Wow');
    super.move();
  }
}
```