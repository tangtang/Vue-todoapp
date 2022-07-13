<template>
  <div class="input-add">
    <input
      type="text"
      name="todo"
      v-model="todoContent"
      @keyup.enter="emitAddTodo"
    />
    <button @click="emitAddTodo">
      <i class="plus"></i>
    </button>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "TodoAdd",
  setup(props, context) {
    const todoContent = ref("");
    const emitAddTodo = () => {
      const todo = {
        id: props.tid,
        content: todoContent.value, //要记得value才能访问里面的值
        completed: false,
      };
      context.emit("add-todo", todo);
      todoContent.value = ""; //清空输入框内容
    };
    return {
      todoContent,
      emitAddTodo,
    };
  },
};
</script>

<style>
/* 添加框 */
.input-add {
  position: relative;
  display: flex;
  align-items: center;
}

.input-add input {
  padding: 16px 52px 16px 18px;
  border-radius: 48px;
  border: none;
  outline: none;
  box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.08);
  width: 100%;
  font-size: 16px;
  color: #626262;
}

.input-add button {
  width: 46px;
  height: 46px;
  border-radius: 50%;
  background: linear-gradient(#c0a5f3, #7f95f7);
  border: none;
  outline: none;

  color: white;
  position: absolute;
  right: 0px;

  cursor: pointer;
}

.input-add .plus {
  display: block;
  width: 100%;
  height: 100%; /* 横线加竖线变成加号按钮 */
  background: linear-gradient(#fff, #fff), linear-gradient(#fff, #fff);
  background-size: 50% 2px, 2px 50%;
  background-position: center;
  background-repeat: no-repeat;
}
</style>
