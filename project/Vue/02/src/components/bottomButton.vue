<template>
    <!-- 如果没有任务就不需要显示底部 -->
    <div class="todo-footer" v-show="total">
            <label>
               <!-- 如果已完成和总的任务数相等那么就勾选 -->
              <!-- <input type="checkbox" :checked="isTotal" @change="selectAll"/> -->
              <input type="checkbox" v-model="isTotal"/>

            </label>
            <span>
              <span>已完成{{doneTotal}}</span> / 全部{{total}}
            </span>
            <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
          </div>
</template>
    
<script >
    export default{
        name:'bottomButton',
        props:['todos',"selectAlltodo","deleteAll"],
        computed:{
            // 用计算属性求解已完成的任务数，可以用reduce遍历累计求和
            doneTotal(){
                return this.todos.reduce((pre,cur) =>pre+(cur.completed?1:0),0)
            },
            // 计算属性判断已完成和总的任务数是否相等
            isTotal:{
                get(){
                    return this.doneTotal === this.todos.length && this.todos.length > 0
                },
                set(e){
                    this.selectAlltodo(e)
                }
            },
            total(){
                return this.todos.length
            }
        },
        methods:{
            clearAll() {
                this.deleteAll()
            }
        }
    }
</script>
    
<style scoped>
    /*footer*/
    .todo-footer {
        height: 40px;
        line-height: 40px;
        padding-left: 6px;
        margin-top: 5px;
    }

    .todo-footer label {
        display: inline-block;
        margin-right: 20px;
        cursor: pointer;
    }

    .todo-footer label input {
        position: relative;
        top: -1px;
        vertical-align: middle;
        margin-right: 5px;
    }

    .todo-footer button {
        float: right;
        margin-top: 5px;
    }
</style>