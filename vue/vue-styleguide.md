# Vue Style Guide
+ 컴포넌트의 이름은 합성어로 사용
  ```js
  Vue.component('todo-item', {
    //
  })
  ```
  ```js
  export default {
    name: 'TodoItem',
    //...
  }
  ```

+ 컴포넌트 데이트는 반드시 함수로 사용
> new Vue를 제외한 모든 컴포넌트의 data 프로퍼티의 값은 반드시 객체를 반환하는 함수이어야 한다.  
> 컴포넌트에서 data가 오브젝트인 경우 모든 인스턴스가 공유한다.  
> 각 컴포넌트의 인스턴스 별로 데이터를 관리하기 위해서 함수로 객체를 반환한다.
  ```js
  Vue.component('todo-item', {
    data: function() {
      return {
        foo: 'bar'
      }
    }
  })
  ```
  ```js
  export default {
    name: 'TodoItem',
    data() {
      return {
        foo: 'bar'
      }
    }
  }
  ```

+ Props는 가능한 상세히 정의한다.
```js
props: {
  status: String
}
```
```js
props: {
  status: {
    type: String,
    required: true,
    validator: function (value) {
      return ['syncing', 'synced', 'version-conflict', 'error'].indexOf(value) !== -1
    }
  }
}
```

+ v-for는 key와 항상 함께 사용한다.
```html
<ul>
  <li v-for="user in users" :key="user.id">
    {{user.name}}
  </li>
</ul>
```

+ v-if와 v-for를 동시에 사용하지 않는다.
> &lt;li v-for="user in users" v-if="shouldShowUsers"> 와 같이 사용하지 않는다.
```html
<ul v-if="shouldShowUsers">
  <li v-for="user in users" :key="user.id">
    {{user.name}}
  </li>
</ul>
```

+ 컴포넌트 스타일 스코프
```html
<templdate>
  <button class="button button-close">X</button>
</templdate>
<style scoped>
.button {
  border: none;
  border-radius: 2px;
}
.button-close {
  background-color: red;
}
</style>
```

```html
<templdate>
  <button :class="[$style.button, $style.buttonClose]">X</button>
</templdate>
<style module>
.button {
  border: none;
  border-radius: 2px;
}
.buttonClose {
  background-color: red;
}
</style>
```

+ 컴포넌트 이름 
  * vue 파일명: 파스칼 표기법
  * 베이스 컴포넌트 이름: Base, App, V 접두어 사용  
    (ex. BaseButton.vue, BaseTable.vue, AppButton.vue, AppTable.vue, VButton.vue, VTable.vue)
  * 싱글인스턴스 컴포넌트 이름: The 접두어를 사용  
    (ex. TheHeading.vue)

+ 다중 속성 엘리먼트 표기 스타일
> 한 라인당 속성 하나로 표기
```html
<img
  src="http://vuejs.org/images/logo.png"
  alt="Vue Logo"
>
<MyComponent
  foo="a"
  bar="b"
  baz="c"
/>
```
