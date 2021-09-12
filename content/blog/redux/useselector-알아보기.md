---
title: useSelector 알아보기
date: 2021-09-12 20:09:24
category: redux
thumbnail: { thumbnailSrc }
draft: false
---

## useSelector
useSelector은 리덕스 스토어의 상태를 조회하는 Hook이다.  
useSelector은 사용할때 해당값들이 하나라도 컴포넌트가 리렌더링된다.

![redux](./img/useSelector1.png)
위의 코드의 경우, login값과 loginError값이 바뀌었을때 리렌더링이 되는 것이다.