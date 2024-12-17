<script setup lang="ts">
import { ref } from 'vue'

const props = defineProps({
  item: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['toggle', 'delete'])

const completed = ref(props.item.completed)
</script>

<template>
  <li class="todo-item">
    <input type="checkbox" v-model="completed" @change="emit('toggle', item)" />
    <span class="text" :class="{ completed }">{{ item.text }}</span>
    <button type="button" @click="emit('delete', item)">Delete</button>
  </li>
</template>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.completed {
  text-decoration: line-through;
  color: #999;
}

.text {
  margin: 0 5px;
  padding: 0 5px;
}
</style>
