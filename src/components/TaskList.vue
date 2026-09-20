<script setup>
import TaskItem from './TaskItem.vue'

defineProps({
  tasks: {
    type: Array,
    required: true
  }
})

const emit = defineEmits([
  'toggle-task',
  'delete-task'
])

function toggleTask(id) {
  emit('toggle-task', id)
}

function deleteTask(id) {
  emit('delete-task', id)
}
</script>

<template>

  <section class="task-list">

    <div
      v-if="tasks.length === 0"
      class="empty-state"
    >

      <div class="empty-icon">
        ✓
      </div>

      <h2>No tasks found</h2>

      <p>
        There are no tasks in this section.
      </p>

    </div>


    <TaskItem
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      @toggle-task="toggleTask"
      @delete-task="deleteTask"
    />

  </section>

</template>