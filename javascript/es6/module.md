# Module

## 설명
ES6에서는 모듈 기능이 표준으로 정의되었다. 브라우저에서는 아직 모듈 문법이 제대로 지원되지 않고 있다.

## 예제
``` javascript
// class.js
export class Animal {
  constructor(name) {
    this.name = name;
  }

  move() {
    console.log(`${this.name} is moved...`);
  }
}

// subclass.js
import { Animal } from './class';

export class Man extends Animal {
  constructor(name) {
    super(name);
  }

  say(msg) {
    console.log(msg);
  } 

  move() {
    console.log('walking...');
    super.move();
  }
}

// app.js
import { Man } from './subclass';

let man = new Man('Jin');

man.say('Hello, World!'); 
man.move(); 
// Hello, World!
// walking...
// Jin is moved...
```