<template>
  <div>
    <ul>
      <li
        class="shadow"
        v-for="( todoItem, index ) in propsdata"
        v-bind:key="todoItem"
      >
        <button
          class="checkBtn"
          v-bind:class="{ checkBtnCompleted: todoItem.completed }"
          v-on:click="toggleComplete(todoItem, index)"
        >
          <i class="fas fa-check"></i>
        </button>
        <span v-bind:class="{ textCompleted: todoItem.completed }">{{ todoItem.item }}</span>
        <button class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
export default {
  props: ['propsdata'],
  methods: {
    removeTodo(todoItem: { item: string, completed: boolean}, index: number) : void {
      this.$emit('removeTodoItem', todoItem, index);
    },
    toggleComplete(todoItem: { item: string, completed: boolean}, index: number) : void {
      this.$emit('toggleTodoItem', todoItem, index);
    },
  },
};
</script>

<style scoped lang="scss">
ul {
  list-style-type: none;
  padding-left: 0;
  margin-top: 0;
  text-align: left;

  li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: .5rem 0;
    padding: 0 .9rem;
    background-color: white;
    border-radius: 5px;

    button {
      border: none;
      background-color: transparent;
      &.checkBtn {
        line-height: 50px;
        color: #62ACDE;
        margin-right: 5px;
      }
      &.checkBtnCompleted {
        color: #B3ADAD;
      }
      &.removeBtn {
        margin-left: auto;
        color: #DE4343;
      }
    }
    .textCompleted {
      text-decoration: line-through;
      color: #B3ADAD;
    }
  }
}

</style>
