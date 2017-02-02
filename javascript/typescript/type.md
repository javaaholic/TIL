# 타입

## 변수 선언

``` typescript
let 변수명: 타입;
```

## 배열 타입

``` typescript
let sports: string[] = ['soccer', 'baseball', 'basketball'];

// 제너릭 사용
let num: Array<number> = [1, 2, 3];
```

## 유니언 타입

``` typescript
let num: string | number = 1;
let bool: string | boolean = true;

console.log(typeof num, num);   // number 1
console.log(typeof bool, bool); // boolean true
```