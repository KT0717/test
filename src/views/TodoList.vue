<script setup lang="ts">
import { ref, watch } from 'vue'
import TodoItem from '@/components/TodoItem.vue'

interface Todo {
  text: string
  completed: boolean
}

const todos = ref<Todo[]>([])
const newTodoText = ref('')

const form = ref<HTMLInputElement | null>(null)

const addTodo = () => {
  console.log("addTodo");
  
  if (newTodoText.value) {
    todos.value.push({
      text: newTodoText.value,
      completed: false
    })
    console.log(todos.value);
    newTodoText.value = ''
  } else {
    form.value.reportValidity()
  }
}

const toggleTodo = (item: Todo) => {
  console.log("toggleTodo", item);
  item.completed = !item.completed
}

const deleteTodo = (item: Todo) => {
  if(!item.completed) return
  const index = todos.value.indexOf(item)
  if (index > -1) {
    todos.value.splice(index, 1)
  }
}

watch(todos,()=>{
  console.log(todos.value);
  
})
</script>

<template>
  <div class="todo-list">
    <h1>Task Management App</h1>
    <form ref="form">
    Task Title:
    <input type="text" v-model.trim="newTodoText" @keyup.enter="addTodo" required />
    <button type="button" @click="addTodo">Add Task</button>

    <ul>
      <TodoItem
        v-for="(item, index) in todos"
        :key="index"
        :item="item"
        @toggle="toggleTodo"
        @delete="deleteTodo"
      />
    </ul>
  </form>
  </div>
</template>

<!-- <style scoped>
.todo-list {
  padding: 20px;
}

.todo-list h1 {
  margin-bottom: 20px;
}
</style> -->
