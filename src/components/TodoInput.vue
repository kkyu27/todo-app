<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" placeholder="Add new things" v-on:keyup.enter="addTodo">
    <span class="addContainer" @click="addTodo">
      +
    </span>
    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고</h3>
      <span slot="footer" @click="showModal = false">할 일을 입력하세요.</span>
    </modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue'
export default {
  data() {
    return {
      newTodoItem: '',
      showModal: false
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== "") {
        var value = this.newTodoItem && this.newTodoItem.trim();
				this.$emit('addTodo', value)
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = '';
    }
  },
  components: {
    Modal
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
  width:85%;
  height:90%;
}
.inputBox input:hover {
  cursor:pointer;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: inline-block;
  width: 3rem;
  height: 100%;
  font-size:25px;
  font-weight:bold;
  color: #fff;
  border-radius: 0 5px 5px 0;
}
.addContainer:hover {
  cursor:pointer;
  opacity: 0.8;
}
</style>