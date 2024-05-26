<template>
  <div id="app">
    <div class="content">
      <Header />
      <Button @task-submitted="addTaskToList" />
      <TaskList :tasks="taskList" @delete-task="deleteTask" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Header from './components/Header.vue'
import Button from './components/Button.vue'
import TaskList from './components/TaskList.vue'

const taskList = ref([])

const addTaskToList = (task) => {
  taskList.value.push(task)
}

const deleteTask = (index) => {
  taskList.value.splice(index, 1);
}
</script>


<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Julius+Sans+One&display=swap');
#app {
  background-image: url('@/assets/background.jpg');
  background-size: cover;
  overflow-y: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.content {
  padding: 20px;
  max-width: 800px;
  height: 100%;
}

</style>