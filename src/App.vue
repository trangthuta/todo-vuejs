<template>
  <div class="app">
    <div class="todo-add">
        <input
      class="todo-list-input"
      type="text"
      placeholder="Add a new task ..."
      v-model="inputTask"
      @keyup.enter="handleAddTodo"
    />
    <button class="todo-list-button" @click="handleAddTodo">
      Add
    </button>
    </div>
    <div class="todo-list">
    <Todo v-for="(todo,index) in todoData" :todo = "todo" :key="index" :index ="index" @handleSelectDeleteTodo = "handleDeleteTodo" @handleSelectEditTodo = "handleEditTodo"/>
  </div>
  </div>
</template>

<script>
// import TodoList from './components/TodoList.vue'
import Todo from './components/Todo.vue'
export default {
  name: 'App',
  components: { Todo },
  data () {
    return {
      inputTask: '',
      todoData: JSON.parse(localStorage.getItem('todos')) === null ? [] : JSON.parse(localStorage.getItem('todos'))

    }
  },
  methods: {
    handleAddTodo () {
      if (this.inputTask) {
        this.todoData.push(this.inputTask)
        this.inputTask = ''
        localStorage.setItem('todos', JSON.stringify(this.todoData))
      }
    },
    handleDeleteTodo (e) {
      this.todoData = this.todoData.filter(item => item !== e)
      localStorage.setItem('todos', JSON.stringify(this.todoData))
    },
    handleEditTodo (todo, index) {
      if (todo === '') {
        alert('Không được để trống  !')
        this.todoData = this.todoData.filter(item => item !== todo)
      } else {
        this.todoData.splice(index, 1, todo)
        localStorage.setItem('todos', JSON.stringify(this.todoData))
      }
    }
  }}
</script>

<style>
.todo-list {
  width: 60%;
  margin: 0 auto;
  margin-top: 50px;
}
body {
  background: #353b48;
  font-size: 16px;
  /* margin : 0 auto */
}
* {
  margin: 0;
  padding: 0;
}
.app {
  /* text-align: center; */
  margin-top: 50px;
}
.todo-list-input {
  border: none;
  outline: none;
  border-bottom: solid 1px #192a56;
  background: #353b48;
  padding: 5px 10px;
  color: #dcdde1;
  margin-right: 20px;
  width : 30%
}
input::placeholder {
  font-size: 12px;
}
.todo-list-button {
  padding: 5px 15px;
  color: #dcdde1;
  background-color: #192a56;
  border-radius: 5px;
  border :none
}
.todo-list-button:hover {
  background-color: green;
}
.todo-add {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
