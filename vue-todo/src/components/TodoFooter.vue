<template>
  <div class="clearAllContainer">
    <button class="clearAllBtn" v-on:click="clearTodo">
      <i class="fas fa-align-slash"></i>
      Clear All
    </button>
  </div>
</template>

<script lang="ts">
export default {
  methods: {
    clearTodo(): void {
      localStorage.clear();
    },
  },
};
</script>

<style scoped lang="scss">
.clearAllContainer {
  display: flex;
  width: 8.5rem;
  height: 50px;
  line-height: 50px;
  background-color: white;
  border-radius: 5px;
  margin: 0 auto;
  vertical-align: middle;
  button {
    background-color: transparent;
    border: none;
    margin: 0 auto;
    &.clearAllBtn {
      color: #e20303;
      display: block;
    }
  }
}
</style>
