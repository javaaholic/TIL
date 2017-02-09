# Linked List

## 설명

연결리스트는 노드로 연결되어 있으며 노드는 원소와 다음 노드를 가리키는 참조로 구성되어 있다. 원하는 값을 얻으려면 헤드에서 부터 참조해야 한다.

## 예제

``` javascript
function LinkedList() {
  
  let head = null,
      length = 0;
  
  function Node(element) {
    this.element = element;
    this.next = null;
  }

  this.append = function (element) {
    let node = new Node(element);

    if (head === null) {
      head = node;
    } else {
      let current = head;

      while (current.next) {
        current = current.next;
      }

      current.next = node;
    }

    length++;
  }

  this.insert = function (element, position) {
    if (position >= 0 && position <= length) {
      let node = new Node(element),
          current = head;
      
      if (position === 0) {
        head = node;
        node.next = current;
      } else {
        let previous;

        for (let i = 0; i < position; i++) {
          previous = current;
          current = current.next;
        }

        previous.next = node;
        node.next = current;
      }

      length++;

      return true;
    } else {
      return false;
    }
  }

  this.removeAt = function (position) {
    if (position >= 0 && position < length) {
      let current = head;
      
      if (position === 0) {
        head = current.next;
      } else {
        let previous;

        for (let i = 0; i < position; i++) {
          previous = current;
          current = current.next;
        }

        previous.next = current.next;
      }

      length--;

      return current;
    } else {
      return null;
    }
  }

  this.remove = function (element) {
    let idx = this.indexOf(element);
    return this.removeAt(idx);
  }

  this.indexOf = function (element) {
    let current = head,
        idx = 0;

    while (current) {
      if (element === current.element) {
        return idx;
      }

      current = current.next;
      idx++;
    }

    return -1;
  }

  this.size = function () {
    return length;
  }

  this.isEmpty = function () {
    return length === 0;
  }

  this.getHead = function () {
    return head;
  }

  this.toString = function () {
    let current = head,
        idx = 0,
        str = '';

    while (current) {
      str += `${idx++}: ${current.element}${current.next ? '\n' : ''}`;
      current = current.next;
    }

    return str;
  }
  
}
``` 