<template>
  <TodoHeader />
  <TodoInput v-on:addTodoItem="addOneItem" />
  <TodoList
    v-bind:propsdata="todoItems"
    v-on:removeTodoItem="removeOneItem"
    v-on:toggleTodoItem="toggleOneItem"
    />
  <TodoFooter />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

interface dataProps {
  todoItems: { item: string, completed: boolean}[],
}
export default defineComponent({
  name: 'App',
  data(): dataProps {
    return {
      todoItems: [],
    };
  },
  methods: {
    addOneItem(newTodoItem: string): void {
      const obj = { completed: false, item: newTodoItem };
      localStorage.setItem(newTodoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem(todoItem: { item: string, completed: boolean}, index: number) {
      console.log(todoItem);
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    toggleOneItem(todoItem: { item: string, completed: boolean}, index: number) {
      this.todoItems[index].completed = !todoItem.completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(this.todoItems[index]));
    },
  },
  created(): void {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i += 1) {
        const key = localStorage.key(i);
        const obj = localStorage.getItem(key || '');
        if (obj && typeof obj === 'string' && key !== 'loglevel:webpack-dev-server') {
          const item: { item: string, completed: boolean } = JSON.parse(obj);
          this.todoItems.push(item);
        }
      }
    }
  },
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter,
  },
});
</script>

<style lang="scss">
body {
  text-align: center;
  background-color: #F6F6F6;
}
#app {
  font-family: "Ubuntu, Helvetica, Consolas";
}
input {
  border-style: groove;
  width: 200px;
}

button {
  border-style: groove;
  cursor: pointer;
}

.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, .03);
}
</style>
