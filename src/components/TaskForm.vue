<script setup>
import { ref } from 'vue'

const taskTitle = ref('')

const emit = defineEmits(['add-task'])

function submitTask() {
  if (taskTitle.value.trim() === '') {
    return
  }

  emit('add-task', taskTitle.value)

  taskTitle.value = ''
}
</script>

<template>

  <form
    class="task-form"
    @submit.prevent="submitTask"
  >

    <input
      v-model="taskTitle"
      type="text"
      placeholder="What do you need to do?"
    />

    <button type="submit">
      <span>+</span>
      Add Task
    </button>

  </form>

</template>