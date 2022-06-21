<script setup>
import {defineAsyncComponent, reactive, provide, ref, onMounted} from "vue"
import ErrorComponent from "./components/ErrorComponent.vue";
import LoadingComponent from "./components/LoadingComponent.vue";
import AsyncComponent from "./components/AsyncComponent.vue"
// 不带选项的异步组件
const Home = defineAsyncComponent(() => import("./view/Home.vue"))

// 带选项的异步组件
/*const AsyncComponent = defineAsyncComponent({
  loader: () => import("./components/AsyncComponent.vue"),
  delay: 300,
  timeout: 3000,
  errorComponent: ErrorComponent,
  loadingComponent: LoadingComponent
})*/
const content = reactive({
  name: 'vue3',
  style: 'composition'
})
function getMessage(data) {
  console.log(data)
}
provide('fromParent', content)

const testEl = ref()
onMounted(() => {
  testEl.value?.helloParent()
})
</script>

<template>
  <Home/>
  <AsyncComponent :data="content" @getMessage="getMessage" ref="testEl"/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
