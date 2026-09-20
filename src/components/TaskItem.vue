<script setup>
defineProps({
  task: {
    type: Object,
    required: true
  }
})

const emit = defineEmits([
  'toggle-task',
  'delete-task'
])
</script>

<template>

  <article
    class="task-item"
    :class="{ completed: task.completed }"
  >

    <button
      class="check-button"
      @click="emit('toggle-task', task.id)"
    >

      <span v-if="task.completed">
        ✓
      </span>

    </button>


    <div class="task-info">

      <h3>
        {{ task.title }}
      </h3>

      <span>
        {{ task.completed ? 'Completed' : 'In progress' }}
      </span>

    </div>


    <button
      class="delete-button"
      @click="emit('delete-task', task.id)"
    >
      🗑
    </button>

  </article>

</template>