<h3>vue.js</h3>

- 컴포넌트 기반의 spa를 구축할 수 있게 해주는 프레임워크



<h3>컴포넌트</h3>

- 웹을 구성하는 로고, 메뉴바, 버튼, 모델창 등 웹 페이지 내의 다양한 ui요소
- 재사용 가능하도록 구조화 한 것

<h3>spa(single page application)</h3>

- 단일 페이지 어플리케이션
- 하나의 페이지 안에서 필요한 영역 부분만 로딩 되는 형태
- 빠른 페이지 변환
- 적은 트래픽 양



초기 vue 만들시

1. vue create <create명>

초기 vue를 만들고 구조설명

- pakage.json

- main.js

  - import { createApp } from 'vue'
    - vue모듈에서 createApp를 가져옴 
  - createApp(App).mount('#app')
    - createApp이라는 함수에 App을 넣어주고, 아이디가 app인 녀석에게 mount를 시키겠다.

- App.vue

  - nav 내에 router-link로 화면의 변화를 줌
  - router-view 는 router라는 폴더 내에 index.js란 파일에 path와 router-link를 맞춰준다면 주소값이 바뀌면서 특정 페이지로 바꾸어주는 역할

- views/HomeView.vue

  - script 내에 특정 파일의 위치를 하나의 변수로 import 시켜주면

  - ```js
    import HelloWorld from '@/components/HelloWorld.vue'
    ```

  - html 요소처럼 tag요소로 사용가능

  - ```html
        <HelloWorld msg="Welcome to Your Vue.js App"/>
    ```

- components/HelloWorld.vue

  - HomeView.vue 에서 import한 vue파일

  - HomeView.vue에서 만든 msg란 요소를 사용가능

  - ```html
        <h1>{{ msg }}</h1>
    ```



<h3>라우터 이해하기</h3>

- App.vue에 router-link에 to='path'를 가지고있음

- 이는 router/index.js에 routes라는 변수로 object([])를 가지고있는데 그 내에 배열({})로 선언되어있는 녀석들중 path와 같아야함

- index.js엔 name이 같으면 안됨

- component란key는 실제 path로 이동시 component에서 가져와 보여 줄 녀석이다.

  - 여기서 component란 ~~.vue란 파일을 의미

  - ```js
    import { createRouter, createWebHistory } from 'vue-router'
    import HomeView from '../views/HomeView.vue'

    const routes = [
      {
        path: '/',
        name: 'home',
        component: HomeView
      },
      {
        path: '/about',
        name: 'about',
        // route level code-splitting
        // this generates a separate chunk (about.[hash].js) for this route
        // which is lazy-loaded when the route is visited.
        component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
      }
    ]
    ```

  - component를 표현하는 방법은 두가지로 나뉘는데 위 코드를 보면 HomeView와 AboutView를 import하는게 다르다

// 예외로

- 함께 프로젝트를 진행하면서 코드규율같은게 있는데 그걸 한번에 해결하기 위해 prettierrc라는 걸 설치했었음

- 근데 이녀석의 규율이너무 빡빡해서 좀 유하게 만들어줘야됨

- package.json과 같은 위치에 .prettierrc라는 파일을 만들고

- ```js
  { "semi": false,
    "bracketSpacing": true,
    "singleQuote": true, 
    "useTabs": false, 
    "trailingComma": "none", 
    "printWidth": 80 }

  // 붙여넣기
  ```

- package.json위치에 "rules" 가 존재하는데

- ```js
   "rules": {"space-before-function-paren": "off"}
     // 붙여넣기
   ```
views 폴더 내에 있는 vue파일 

- views에 존제하는 .vue파일은 화면전체를 차지하는 component가 들어온다 보면 됨(하나의 페이지를 정의한다 생각하자)

components폴더 내에 있는 vue파일

- 이 안에 있는 component(.vue파일)는 재사용이 가능한 component는 components라는 폴더 내에 만들자

파일 네임에 대한 룰

- 화면전체 페이지에 해당하는 component는(views폴더 내에 있는 component) 네이밍 뒤에 View라는 이름을 붙여준다
- components폴더 내에 있는 component는



views폴더내에 vue파일을 만들때

```html
<template>
<!-- html태그? 요소는 다 template에 넣어줌 -->
</template>

<script>
export default {
  data() {
    return {
      userName: 'John Doe'
    }
  }
}
</script>
```

#css 적용시 팁

- if 하나의 components에서만 적용되는 css style을 만들고 싶다면

- ```
  <style scoped>

  </style>
  ```

- 전체 적용되는 style을 만들고싶다면

- ```
  <style>

  </style>
  ```

- ​