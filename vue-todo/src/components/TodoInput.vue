<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <button class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn" />
    </button>
    <!-- use the modal component, pass in the prop -->
    <transition name="modal">
    <Modal v-show="showModal" @close="showModal = false">
      <!--
        you can use custom content here to overwrite
        default content
      -->
      <template v-slot:header>
        <h3>Warning!</h3>
        <button class="closeModalBtn" @click="showModal = false;">
          <i class="fas fa-times"></i>
        </button>
      </template>
      <template v-slot:body>
        Type Todo Title!!
      </template>
    </Modal>
    </transition>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Modal from './common/Modal.vue';

interface dataProps {
  newTodoItem: string,
  showModal: boolean,
}
export default defineComponent({
  data: (): dataProps => ({
    newTodoItem: '',
    showModal: false,
  }),
  methods: {
    addTodo(): void {
      if (this.newTodoItem !== '') {
        this.$emit('addTodoItem', this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = true;
      }
    },
    clearInput(): void {
      this.newTodoItem = '';
    },
  },
  components: {
    Modal,
  },
});
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

.closeModalBtn {
  position: absolute;
  top: 5px;
  right: 5px;
  color: #42B983;
  background-color: transparent;
  border: none;
  cursor: pointer;
}

</style>
