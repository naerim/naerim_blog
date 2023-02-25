---
title: Array every()와 some()
date: 2023-02-25 23:02:62
category: javascript
thumbnail: { thumbnailSrc }
draft: false
---

코테 문제를 풀다가 every()와 some()이 헷갈려서 다시 공부해보고자 한다!

## every()와 some()

every()는 모든 요소에 대해서 조건을 충족해야 true를 리턴하고 some()은 1개 요소만 충족해도 true를 리턴한다.

## every()

```javascript
const isBelowThreshold = v => v < 40
const arr = [1, 30, 39, 29, 10]
console.log(arr.every(isBelowThreshold))
// true
```

주어진 판별 함수의 조건을 모두 통과했기 때문에 true를 반환한다.

## some()

```javascript
const arr = [1, 2, 3, 4, 5]
const even = e => e % 2 === 0
console.log(arr.some(even))
// true
```

주어진 판별 함수를 적어도 하나라도 통과하기 때문에 true를 반환한다.
