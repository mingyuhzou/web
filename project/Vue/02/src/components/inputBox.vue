<template>
    <div class="todo-header">
        <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="addEle"/>
      </div> 
</template>
    
<script >
    import {nanoid} from 'nanoid'
    export default{
        name:'inputBox',
        data(){
            return {
                // 通过双向数据绑定获取键盘输入
                title:''
            }
        },
        props:["receive"],
        methods:{
            addEle(){
                // 简单判断
                if(!this.title) return 
                
                //  根据输入生成一个todo对象，这里因为是单机版的所以ID序列号只能自己定义，通过nanoid(uuid的简化版，可以生成唯一序列号)实现
                //  这个对象要传递给todolist组件一个最初级的方法是把todos放到app组件上,app组件将todos传入itemList组件，在app中
                //  实现一个操作todos的方法然后传给inputBox组件，这样就能在inputBox组件中修改itmeLists组件中的todos了
                const obj={id:nanoid(),title:this.title,completed:false}

                // 调用函数添加数据
                this.receive(obj)

                // 注意清空数据
                this.title=''
            }
        }
    }
</script>
    
<style scoped>
    /*header*/
    .todo-header input {
        width: 560px;
        height: 28px;
        font-size: 14px;
        border: 1px solid #ccc;
        border-radius: 4px;
        padding: 4px 7px;
    }

    .todo-header input:focus {
        outline: none;
        border-color: rgba(82, 168, 236, 0.8);
        box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
    }

</style>