<template>
  <main>
    <div class="container">
      <h1>欢迎使用 orange 待办事项</h1>
      <todo-add :tid="todos.length" @add-todo="addTodo"/>
      <!-- 过滤选项传递给todo-filter组件，监听change-filter属性 -->
      <todo-filter :selected="filter" @change-filter="filter = $event" />
      <!-- 显示过滤后的数组 -->
      <todo-list :todos="filteredTodos" />
    </div>
  </main>
</template>

<script>
import { computed,ref }  from "vue";
import TodoAdd from './components/TodoAdd.vue';
import TodoFilter from './components/TodoFilter.vue';
import TodoList from './components/TodoList.vue';

export default {
  name: "App",
  components: { TodoAdd, TodoFilter, TodoList },
  setup (){
    const todos = ref([]);//包装一个空数组，来作为默认todo列表的数据
    const addTodo = (todo) => todos.value.push(todo);

    const filter = ref("all");//选项默认为all

    //根据filter的值过滤列表，把过滤好的数组放到filter.todos变量中
    const filteredTodos = computed(() => {
      switch (filter.value){
        case "done":
          return todos.value.filter((todo) => todo.completed);
        case "todo":
         return todos.value.filter((todo) => !todo.completed)
         default:
          return todos.value;
      }
    });
  
    return { //在temp中使用函数和数据，要以对象的形式返回
      todos,
      addTodo,
      filter,
      filteredTodos,
    };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Helvetica, "PingFang SC", "Microsoft Yahei", sans-serif;
}

/* 整个页面样式 */
main {
  width: 100vw;
  min-height: 100vh;
  display: grid;
  align-items: center;
  justify-items: center;
  background: rgb(203,210,240);
}

.container {
  width: 60%;
  max-width: 400px;
  box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.15);
  border-radius: 24px;
  padding: 18px 28px;
  background-color: white;
}

/* 标题 */
h1 {
  margin: 24px 0;
  font-size: 28px;
  color: #414873;
}





</style>
