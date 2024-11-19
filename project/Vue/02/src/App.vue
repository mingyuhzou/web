<template>
    <div id="root">
      <div class="todo-container">
        <div class="todo-wrap">
          <inputBox :receive="receive"/>
          <itemList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
          <bottomButton :todos="todos" :selectAlltodo="selectAlltodo" :deleteAll="deleteAll"/>
        </div>
      </div>
    </div>

</template>

<script>
  import inputBox from './components/inputBox.vue';
  import bottomButton from './components/bottomButton.vue';
  import itemList from './components/itemList.vue';

  export default {
    name: 'App',
    data(){
      return {
        // 数据放在App中共享，这样可以用props传递给所有的子组件使用，所有对数据的操作方法同时都放在App中，通过props给子组件调用
          todos:[
              {id:'001',title:'打搅',completed:false},
              {id:'002',title:'coding',completed:false},
              {id:'003',title:'睡觉',completed:true}
          ]
      }
    },
    methods:{
      
      // 添加item
      receive(x){
        // 用数组方法才能触发数据检测
        this.todos.unshift(x)
      },

      // 勾选复选框时修改Value
      checkTodo(id){
        this.todos.forEach(todo => {
          if (id===todo.id){
              todo.completed=!todo.completed
          }
        }
      );
      
      },

      // 删除任务 使用filter函数
      deleteTodo(id){
        this.todos=this.todos.filter(item=>item.id!==id)  
      },
      deleteAll() {
        this.todos = this.todos.filter(ele => { 
          return !ele.completed
        })
      },

      // 实现全选或全不选
      selectAlltodo(isAll) {
        this.todos.map((ele) => { 
          if (isAll && !ele.completed) ele.completed = !ele.completed
          else if (!isAll&&ele.completed) ele.completed=!ele.completed
        })
      }

    },
    components:{inputBox,bottomButton,itemList}
}
</script>

<style>
  /*base*/
  body {
    background: #fff;
  }

  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }

  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }

  .btn:focus {
    outline: none;
  }

  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }

  





</style>
