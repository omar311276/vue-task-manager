<script setup>
import { ref, computed } from 'vue'

import TaskForm from './components/TaskForm.vue'
import TaskList from './components/TaskList.vue'

const tasks = ref([
  {
    id: 1,
    title: 'Learn Vue',
    completed: false
  },
  {
    id: 2,
    title: 'Build a Vue project',
    completed: false
  },
  {
    id: 3,
    title: 'Practice JavaScript',
    completed: true
  }
])

const filter = ref('all')

function addTask(title) {
  if (title.trim() === '') return

  tasks.value.push({
    id: Date.now(),
    title: title,
    completed: false
  })
}

function toggleTask(id) {
  const task = tasks.value.find(item => item.id === id)

  if (task) {
    task.completed = !task.completed
  }
}

function deleteTask(id) {
  tasks.value = tasks.value.filter(item => item.id !== id)
}

const filteredTasks = computed(() => {
  if (filter.value === 'active') {
    return tasks.value.filter(item => !item.completed)
  }

  if (filter.value === 'completed') {
    return tasks.value.filter(item => item.completed)
  }

  return tasks.value
})

const remainingTasks = computed(() => {
  return tasks.value.filter(item => !item.completed).length
})
</script>

<template>
  <main class="app">

    <header class="header">
      <div>
        <span class="small-title">MY WORKSPACE</span>

        <h1>Task Manager</h1>

        <p>
          Organize your tasks and stay productive.
        </p>
      </div>

      <div class="task-counter">
        <strong>{{ remainingTasks }}</strong>
        <span>remaining</span>
      </div>
    </header>


    <TaskForm @add-task="addTask" />


    <nav class="filters">

      <button
        :class="{ active: filter === 'all' }"
        @click="filter = 'all'"
      >
        All
      </button>

      <button
        :class="{ active: filter === 'active' }"
        @click="filter = 'active'"
      >
        Active
      </button>

      <button
        :class="{ active: filter === 'completed' }"
        @click="filter = 'completed'"
      >
        Completed
      </button>

    </nav>


    <TaskList
      :tasks="filteredTasks"
      @toggle-task="toggleTask"
      @delete-task="deleteTask"
    />

  </main>
</template>