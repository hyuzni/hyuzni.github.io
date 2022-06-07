---
layout: post
title: setting vite vue3 vue-router
categories: study
tags: [study]
---

## 1. vite + vue3 설치하기

> 공식 문서를 참고

[vite-vue3 공식문서](https://vitejs.dev/guide/#scaffolding-your-first-vite-project, Vite App)
   
{% highlight sh %}
# npm 6.x
npm create vite@latest my-vue-app --template vue

# npm 7+, extra double-dash is needed:
npm create vite@latest my-vue-app -- --template vue
{% endhighlight %}

끝! 확실히 webpack 쓰는것보다 훨씬 easy~   

## 2. vue router 설정
   
> 얘도 공식문서 우선 참고

[vue-router 설치](https://router.vuejs.org/installation.html, vue-router)
   
{% highlight sh %}
npm install vue-router@4
{% endhighlight %}
   
> router 설정파일 생성
.src/router.js 로 생성. 이건 어떤방식으로 생성하든 자유.   
router의 사용은 router-view, router-link 로 사용할 수 있음.

{% highlight html %}
  # 아래 문법은 파일 빌드 될 때 a 태그로 표현 됨
  <router-link to="/">Go to Home</router-link>
  <router-link to="/about">Go to About</router-link>

  # 아래는 라우터로 호출되는 컴포넌트 파일이 render 됨
  <router-view></router-view>
{% end highlight %}

공식 문서를 참고한 router.js 작성   
{% highlight router.js %}
// vue-router 를 쓰기 위해선 'VueRouter'로 선언이 되어있어야 하는데 vue3 부터는 에러발생.
// 그래서 바꿔서 선언해줌.
// import VueRouter from 'vue-router'
import { createRouter, createWebHistory } from 'vue-router'

// 1. Define route components.
// These can be imported from other files
const testTemplate = { template: '<div>TestPage</div>' } // 직접 작성 방식
import importTemplate from './components/HelloWorld.vue' // component template import 

// 2. Define some routes
// Each route should map to a component.
// We'll talk about nested routes later.
const routes = [
    // 한번만 쓰는 component라면 아래처럼 쓰는법을 추천
    { path: '/', component: () => import('./components/HelloWorld.vue') }, 
    { path: '/test', component: testTemplate }, // 이건 왜 안되는지 모르겠음
    { path: '/import', component: importTemplate } 
]

// 3. Create the router instance and pass the `routes` option
// You can pass in additional options here, but let's
// keep it simple for now.
// 이게 공식문서에 작성되어있는 createRouter 방법인데, 안되서 import 방식 바꾸고 아래처럼 변경
const router = VueRouter.createRouter({
  // 4. Provide the history implementation to use. We are using the hash history for simplicity here.
  history: VueRouter.createWebHashHistory(),
  routes, // short for `routes: routes`
})

const router = createRouter({
    history: createWebHistory(), // history: createRouter 작성 시 필수 속성.
    routes
})

export default router; // 여기서 export 해줌으로 router.js는 끝.
{% end highlight %}

여기까지가 router.js의 내용.   
아래 내용은 vite 로 vue create 생성시 만들어진 main.js에서 작성.   

{% highlight main.js %}
import router from './router.js' // 우선 연결해줄 router 파일의 import 

// 5. Create and mount the root instance.
const app = Vue.createApp({})
// Make sure to _use_ the router instance to make the
// whole app router-aware.
app.use(router)

app.mount('#app')

// 위에 공식문서의 내용을 체이닝해서 아래처럼 작성할 수 있음.!
createApp(App).use(router).mount('#app')

// Now the app has started!
{% end highlight %}
   
## 3. 추가 설정

> alias '@' -> './src' 경로설정
{% highlight vite.config.js %}

import path from 'path' // path 설정을 위한 import 

export default defineConfig({
  plugins: [vue()],
  // alias 로 '@'를 './src' 경로로 지정하여 사용하기위해 아래처럼 추가.
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src')
    }
  }
})
{% endhighlight %}
   
여기까지 작성하고 추가적인 내용은 따로 포스트 써야징