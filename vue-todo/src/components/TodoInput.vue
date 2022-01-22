<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <button class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn" />
    </button>
  </div>
</template>

<script lang="ts">
export default {
  data: (): {newTodoItem: string} => ({
    newTodoItem: '',
  }),
  methods: {
    addTodo(): void {
      localStorage.setItem(this.newTodoItem, this.newTodoItem);
      this.clearInput();
    },
    clearInput(): void {
      this.newTodoItem = '';
    },
  },
};
</script>

<style scpoed lang="scss">

.inputBox {
  background-color: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;

  > input {
    border-style: none;
    font-size: .9rem;
    width: calc(100% - 50px);
    margin: 0;
    float: left;
    padding: 0px;
    height: 100%;
    box-sizing: border-box;
  }

  input:focus {
    outline: none;
  }
}

.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
  border: none;
  height: inherit;
}

.addBtn {
  color: white;
  // vertical-align: middle;
}

</style>
