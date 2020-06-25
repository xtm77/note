# vue.js 완벽가이드

## 프로젝트 생성
```sh
vue create 프로젝트명
```

  ## vue-router
  1. 설치
  > 프로젝트 디렉토리에서 아래와 같이 입력한다.
  ```sh
  vue add router
  ```
  2. dynamic router matching

  ## vuex
  1. 설치
  > 프로젝트 디렉토리에서 아래와 같이 입력한다.
  ```sh
  vue add vuex
  ```
  2. vuex 상태도  
  ![vuex 상태](./images/vuex-state.png)
      + state
      ```json
      state: {
        mydata: [],
      }
      ```
      + actions
        ```js
        actions: {
          FETCH_XXX(context) {
            context.commit('SET_XXX', data);
          }
        }
        ```
      + mutations
      ```js
      mutations: {
        SET_XXX(state, data) {
          state.mydata = data;
        }
      }
      ```
      + getters
      ```js
      getters: {
        getXXX(state) {
          return state.xxx;
        },
        fetchXXX(state) {
          return state.xxx;
        }
      }
      ```

  2. 모듈화
      + mutations.js
      + actions.js
  3.  aaa

  ## vuetify
  1. 

## 트랜지션
[트랜지션](https://kr.vuejs.org/v2/guide/transitions.html)


## hoc and mixin
### HOC
### Mixin
---
## 데이터 호출 시점
### 라이프 사이클 훅
### 라우터 네비게이션 가드
---

## 비동기처리
### async
### await

