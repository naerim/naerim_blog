---
title: 동기적 vs 비동기적
date: 2021-09-12 20:09:83
category: etc
thumbnail: { thumbnailSrc }
draft: false
---

## 동기적
어떤 작업을 요청했을 때, 그 작업이 종료될때 까지 기다린 후 다음 작업을 수행

## 비동기적
어떤 작업을 요청했을 때, 그 작업이 종료될때 까지 기다리지 않고 다른 작업을 하고 있다가, 요청했던 작업이 종료되면 그에 대한 추가 작업을 수행하는 방식

## [문제해결] switi에서 동기적 처리순서를 이용한 해결방법
```typescript
const fetchOnlineStudyList = (order: boolean, query: string) =>  dispatch(onlineStudyListRequest(order, query));
const fetchOfflineStudyList = (order: boolean, query: string) => dispatch(offlineStudyListRequest(order, query));

const { onlineStudyList, offlineStudyList } = useSelector(
  (state: rootState) => state.studyReducer
);
```

```typescript
useEffect(() => {
    let tag = '';
    tagList.forEach(({ key, name, category }) => {
      if (category == 'interest') {
        // 카테고리
        if (tag.includes('category')) tag += ':' + (key + 1).toString();
        else tag += '&category=' + (key + 1).toString();
      } else if (category == 'region') {
        // 지역
        if (tag.includes('region')) tag += ':' + (key + 1).toString();
        else tag += '&region=' + (key + 1).toString();
      } else {
        // 모집대상
        if (tag.includes('state')) tag += ':' + (key + 1).toString();
        else tag += '&state=' + (key + 1).toString();
      }
    });
    setQuery(tag);
}, [tagList]);

useEffect(() => {
    fetchOnlineStudyList(checked, query);
    fetchOfflineStudyList(checked, query);
    idx === 0 ? setContent(onlineStudyList) : setContent(offlineStudyList);
}, [query]);
```
비동기적 처리 -> 동기적 처리 순서를 사용해서 선택한 태그값으로 리스트가 필터링되지 않았었다. 
이를 동기적 처리를 사용해서 해결했다.
  
------- 해결코드
```typescript
useEffect(() => {
    let tag = '';
    tagList.forEach(({ key, name, category }) => {
      if (category == 'interest') {
        // 카테고리
        if (tag.includes('category')) tag += ':' + (key + 1).toString();
        else tag += '&category=' + (key + 1).toString();
      } else if (category == 'region') {
        // 지역
        if (tag.includes('region')) tag += ':' + (key + 1).toString();
        else tag += '&region=' + (key + 1).toString();
      } else {
        // 모집대상
        if (tag.includes('state')) tag += ':' + (key + 1).toString();
        else tag += '&state=' + (key + 1).toString();
      }
    });
    console.log('category test ......', tag);
    setQuery(tag);
}, [tagList]);

useEffect(() => {
    console.log(query);
    fetchOnlineStudyList(checked, query);
    fetchOfflineStudyList(checked, query);
}, [query]);

useEffect(() => {
  idx === 0 ? setContent(onlineStudyList) : setContent(offlineStudyList);
}, [idx, onlineStudyList, offlineStudyList]);
```
