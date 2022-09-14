<template>
  <div class="todo">
    <input type="text" v-model="todo" class="todo-item-content" ref="input" @change="handleSelectEditTodo(todo ,index)"/>
    <i class="fa-solid fa-trash-can" @click="handleSelectDeleteTodo(todo)"></i>
    <i class="fa-solid fa-pen-to-square" @click="handleFocusTodo(todo)"></i>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: ['todo', 'index'],
  methods: {
    handleFocusTodo () {
      this.$refs.input.focus()
    },
    handleSelectDeleteTodo (e) {
      this.$emit('handleSelectDeleteTodo', e)
    },
    handleSelectEditTodo (a, b) {
      this.$emit('handleSelectEditTodo', a, b)
    }
  }
}
</script>

<style scoped>
.todo {
  background-color: #192a56;
  margin: 0 auto;
  padding: 10px 0;
  border-left: 5px solid #c23616;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  position: relative;
  margin-bottom: 10px;
}
.todo-item {
  color: #dcdde1;
  margin: 20px 0;
  /* background-color: #192a56; */
  padding: 10px 0;
  border-left: 5px solid #c23616;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  width: 100%;
}
.todo-icon {
  position: absolute;
  z-index: 1999;
  right: 10px;
}
.todo-item-content {
  background-color: #192a56;
  outline: none;
  border: none;
  color: #dcdde1;
  width: 93%;
  height: 100%;
  padding-left: 10px;
  /* background-color: red; */
}
.fa-solid {
  font-size: 15px;
}
.fa-trash-can {
  color: #c23616;
  margin-right: 10px;
}
.fa-pen-to-square {
  color: #4cd137;
}
</style>
