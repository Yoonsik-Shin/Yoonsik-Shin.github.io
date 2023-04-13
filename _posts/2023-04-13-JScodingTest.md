---
layout: single
title: "JS 코딩테스트 문법정리"
categories: 코딩테스트
tag: [JavaScript, 코딩테스트]
toc: true
author_profile: false
sidebar:
  nav: "counts"
use_math: true
---

# [javascript] 코딩테스트 문법 정리

​

<div class="notice--secondary">
  <h4>
    파이썬과 다른 부분만 따로 정리해놓는 시리즈입니다.
  </h4>
</div>

### 몫만 남기기

- 파이썬 : `//` 활용
- JS : `parseInt( / )` 활용

```js
console.log(parseInt(a / b));
```

### 빠른 출력

- 일반적인 출력 과정만으로 시간 초과를 받을 수 있는 상황일 때 활용하는 기법
- 줄바꿈`\n`을 사용하여 하나의 문자열로 정답을 출력하면 출력시간을 단축할 수 있음

```js
let ans = "";

// not good
for (let i = 1; i <= 10000; i++) {
  console.log(i);
}

// good ✔️
for (let i = 1; i <= 10000; i++) {
  ans += i + "\n";
}
console.log(ans);
```

> Good case : ![image-20230413103555441]({{site.url}}/images/image-20230413103555441.png)
>
> Bad case : ![image-20230413103637540]({{site.url}}/images/image-20230413103637540.png)

​

### 실행시간측정

- `console.time('작명')`과 `console.timeEnd('작명')`사이에 측정하고 싶은 코드를 넣어주면 실행시간을 측정해줌

```js
console.time("check");

for (let i = 1; i <= 10000; i++) {
  console.log(i);
}

console.timeEnd("check");
```

​

### 입력받기

#### fs 모듈

- 입력데이터가 **텍스트 파일**로 주어지는 경우 사용
- 백준 문제풀이시 사용

```js
// commonjs
let fs = require("fs");

// ES6
import fs from "fs";

let input = fs
  .readFileSync("파일명") // 전체 텍스트 읽어오기
  .toString() // 객체를 문자열로 변환해주기
  .split("\n"); // `\n`을 기준으로 나눠 리스트로 반환받기
```

```bash
# input.txt
123
456
789
10000
```

![image-20230413105129495]({{site.url}}/images/image-20230413105129495.png)

> 백준에서 입력받기

```js
const fs = require("fs");

let input = fs
  .readFileSync("/dev/stdin") // 전체 텍스트 읽어오기
  .toString() // 객체를 문자열로 변환해주기
  .split("\n"); // `\n`을 기준으로 나눠 리스트로 반환받기
```

​

#### readline 모듈

- fs 모듈을 이용할 수 없을 경우 사용
- **한 줄씩** 입력을 받을 때 사용
- 구문을 통채로 외워야함

```js
// commonjs
const rl = require("readline");

// ES6
import readline from "readline";

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

let input = [];
rl.on("line", (line) => {
  // 입력 시작
  input.push(line);
}).on("close", () => {
  // 입력 종료 => Ctrl + C
  console.log(input);
  process.exit();
});
```

![image-20230413111303768]({{site.url}}/images/image-20230413111303768.png)

​

### 데이터 형변환

- `Number`와 `String` 활용

```js
// 문자열 >> 숫자
let a = "2023";
let b = Number(a);

// 숫자 >> 문자열
let c = 1004;
let d = String(c);
```

​

### Reduce

- **배열**의 **모든 원소**에 **연산**을 **순차적**으로 적용할 때 사용

```js
// 배열 내에서 최소값 구하기
let minVal = data.reduce((a, b) => Math.min(a, b));
```

```js
// 배열의 합 구하기
let total = data.reduce((a, b) => a + b);
```

​

### 배열 초기화

1. 직접 값을 설정하여 초기화

```js
let arr = [1, 2, 3, 4, 5];
```

2. 길이가 10이고, 모든 값이 0인 배열 초기화

```js
let arr = new Array(10).fill(0);
```

​

### 집합 자료형

- 특정 값이 있는지 없는지 없는 확인할때 사용

```js
let newSet = new Set();

// 값 삽입
newSet.add(1);
newSet.add(2);
newSet.add(3);

// 개수 [.size]
console.log(newSet.size);

// 포함여부 [.has(포함여부를 체크할 )]
console.log(newSet.has);

// 값 제거
newSet.delete(삭제할값);

// 값 하나씩 출력하기
for (let i of newSet) {
  console.log(i);
}
```

​

### 반올림

- `toFixed() `메서드를 활용

```js
// 소수점 아래 3자리까지 출력하고, 4자리 숫자를 기준으로 반올림됨
let a = 20.2345;
console.log(a.toFixed(3)); // 20.235

let b = 20.2344;
console.log(b.toFixed(3)); // 20.234
```
