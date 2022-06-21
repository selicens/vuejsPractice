<template>
    <div>ref相关</div>
    <input type="number" v-model="model">
    <button v-on:click="model++">+</button>
    <p>ref响应式的值：{{model}}</p>
    <p>解构后会失去响应式：{{value}}</p>
    <div>reactive相关</div>
    <p>reactive响应式的值：{{list.item.name}}-{{list.item.content}}</p>
    <p>解构后会失去响应式：{{item.name}}-{{item.content}}</p>
    <p>使用toRefs使其拥有响应式：{{item2.name}}-{{item2.content}}</p>
    <button v-on:click="updateList">更新</button>
    <div v-for="item in arrList">
        {{item.name}}-{{item.content}}
    </div>
</template>

<script setup name="Home">
    import {ref, toRefs, reactive, onBeforeUpdate, onUpdated} from 'vue'
    let model = ref(0)
    const {value} = model

    let list = reactive({
        item: {name: 'vue3', content: 'composition'}
    })
    const {item} = list
    const {item:item2} = toRefs(list)
    function updateList () {
       list.item = {name: 'vue2', content: 'options'}
    }

    let arrList = reactive([
        {name: 'vue3', content: 'composition'},
        {name: 'vue2', content: 'options'}
        ])
</script>

<style scoped>

</style>
