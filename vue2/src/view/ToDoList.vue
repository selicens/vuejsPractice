<template>
    <div>
        <input type="text" placeholder="请输入" v-model="model"/>
        <button type="submit" v-on:click="onsubmit">确定</button>
        <ul>
            <li v-for="item in list" v-bind:key="item.id">
                <input type="checkbox" v-model="item.done">
                {{item.name}}-{{item.content}}
                <button v-on:click="onupdate(item)">修改</button> |
                <button v-on:click="ondelete(item)">删除</button>
            </li>
        </ul>
        <div>
            <input type="checkbox" :checked="checkNum === num ? true : false" v-on:click="allChecked" ref="allCheck">
            <span>已选择{{checkNum}}/总数{{num}}</span>
            <input type="checkbox" @click="orderAsc"><span>升序</span>
            <input type="checkbox" @click="orderDes"><span>降序</span>
        </div>
    </div>
</template>

<script>
    export default {
        name: "ToDoList",
        data() {
            return {
                model: '',
                list: [
                    {id: '0', name: 'vue', content: 'vue3再续前缘', done: true},
                    {id: '1', name: 'react', content: 'react18王者归来', done: false},
                    {id: '2', name: 'angular', content: 'angular雄风依在', done: true}
                ],
                checkedModel: '',
                hoverState: false
            }
        },
        computed: {
            random(){
                return Math.random()
            },
            num() {
                return this.list.length
            },
            checkNum() {
                const val = this.list.filter(item => {
                    return item.done === true
                })
                return val.length
            }
        },
        methods: {
            onsubmit() {
                console.log(this.model)
                const random = this.random
                const data = {id: random, name: this.model, content: '也许只是一个意外', done: false}
                this.list.push({...data})
            },
            onupdate(el) {
                this.list.forEach(item => {
                    if (item === el){
                        item.content = this.model
                    }
                })
            },
            ondelete(el) {
                this.list = this.list.filter(item => {
                    if (item !== el) {
                        return item
                    }
                })
            },
            allChecked(){
                const state = this.$refs.allCheck.checked
                console.log(state)
                this.list.forEach(item => {
                    item.done = state ? true : false
                })
            },
            orderAsc() {
                this.list = this.list.sort((a, b) => a.id-b.id)
            },
            orderDes() {
                this.list = this.list.sort((a, b) => b.id-a.id)
            }
        }
    }
</script>

<style scoped>
    input::placeholder{
        color: red;
    }
    div{
        border: 1px solid #cccccc;
        width: 500px;
    }
    ul, li{
        list-style: none;
        text-align: left;
    }
    ul{
        border: 1px solid pink;
    }
    li:hover{
        background-color: pink;
    }
</style>
