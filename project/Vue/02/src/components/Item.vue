<template>
    <li>
        <label>         
            <!-- 绑定change事件 勾选时会触发handleCheck，handleCheck内调用App中的checkTodo来修改值-->
            <input type="checkbox" :checked="obj.completed" @change="handleCheck(obj.id)"/>
             <span>{{obj.title}}</span>
        </label>
        <button class="btn btn-danger" @click="deleteItem(obj.id)" >删除</button>
    </li>
</template>
    
<script >
    export default{
        name:'li-item',
        props:['obj','checkTodo','deleteTodo'],
        methods:{
            handleCheck(id){
                this.checkTodo(id)
            },
            deleteItem(id){
                if(confirm('确定删除吗?')){
                    this.deleteTodo(id)
                }
            }
        },
        mounted(){
            console.log(this.obj)
        }
    }
</script>
    
<style scoped>
    /*item*/
    li {
        list-style: none;
        height: 36px;
        line-height: 36px;
        padding: 0 5px;
        border-bottom: 1px solid #ddd;
    }

    li label {
        float: left;
        cursor: pointer;
    }

    li label li input {
        vertical-align: middle;
        margin-right: 6px;
        position: relative;
        top: -1px;
    }

    li button {
        float: right;
        display: none;
        margin-top: 3px;
    }

    li:before {
        content: initial;
    }

    li:last-child {
        border-bottom: none;
    }
    li:hover{
        background-color: #ccc;
    }
    li:hover button{
        display: block;
    }

</style>