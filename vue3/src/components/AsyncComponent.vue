<template>
    <div>异步组件，通过defineAsyncComponent加载</div>
    <p>prop: {{props.data}}</p>
    <button @click="setMessage">emit向父组件传递</button>
    <p>provide/inject: {{fromParent}}</p>
</template>
<script>
    export default{
        name: 'AsyncComponent'
    }
</script>
<script setup>
   import {ref, inject,useSlots, useAttrs} from 'vue'
    const props = defineProps({
        data: {
            name: String,
            style: String
        }
    })
   const emits = defineEmits(['getMessage'])
    const setMessage = () =>{
       emits('getMessage', '来自emit传递的消息')
    }
    const fromParent = inject('fromParent')
    const helloParent = () => {
        console.log('hello')
    }
    defineExpose({helloParent})
    const attrs = useAttrs()
   const slots = useSlots()
   console.log(attrs, slots)
</script>

<style scoped>

</style>
