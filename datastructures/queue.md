# Queue

## 설명

FIFO(First In First Out)의 원리를 따르는 정렬된 컬렉션이다. 먼저 들어간 자료가 먼저 나온다.

## 구현

``` javascript
class Queue {
  constructor() {
    this.items = [];
  }

  enqueue(element) {
    this.items.push(element);
  }

  dequeue() {
    return this.items.shift();
  }

  front() {
    return this.items[0];
  }

  size() {
    return this.items.length;
  }

  isEmpty() {
    return this.items.length === 0;
  }

  clear() {
    this.items = [];
  }

  print() {
    console.log(this.items.toString());
  }
}
```

## 예제

``` javascript
// 우선순위 큐
class Queue {
  constructor() {
    this.items = [];
  }

  enqueue(element, priority) {
    let queueElement = { element, priority },
        added = false;

    for (let idx in this.items) {
      if (queueElement.priority < this.items[idx].priority) {
        this.items.splice(idx, 0, queueElement);
        added = true;
        break;
      }
    }

    if (!added) {
      this.items.push(queueElement);
    }
  }

  dequeue() {
    return this.items.shift();
  }

  front() {
    return this.items[0];
  }

  size() {
    return this.items.length;
  }

  isEmpty() {
    return this.items.length === 0;
  }

  clear() {
    this.items = [];
  }

  print() {
    for (let value of this.items) {
      console.log(`${value.priority} - ${value.element}`);
    }
  }
}
```