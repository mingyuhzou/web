<template>
    <div>
    <ul class="todo-main">
        <!-- v-for指令列表渲染 将键值绑定为唯一的id todo对象和checkTodo方法用props传入给item组件 App想传递函数给item目前只能层层传递-->
        <itemElement v-for="todo in todos" :key="todo.id" :obj="todo" :checkTodo="checkTodo" :deleteTodo="deleteTodo" />
    </ul>  
    </div>
</template>
    
<script >
    import itemElement from './Item.vue';
    export default{
        name:'itemList',

        props:["todos", "checkTodo","deleteTodo"],
        mounted(){
            console.log(this.todos)
        },
        components:{itemElement}
    }
</script>
    
<style scoped>
    /*main*/
    .todo-main {
        margin-left: 0px;
        border: 1px solid #ddd;
        border-radius: 2px;
        padding: 0px;
    }

    .todo-empty {
        height: 40px;
        line-height: 40px;
        border: 1px solid #ddd;
        border-radius: 2px;
        padding-left: 5px;
        margin-top: 10px;
    }
</style>