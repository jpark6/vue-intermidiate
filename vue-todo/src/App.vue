<template>
  <TodoHeader />
  <TodoInput />
  <TodoList />
  <TodoFooter />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default defineComponent({
  name: 'App',
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
