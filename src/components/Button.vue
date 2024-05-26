<template>
  <div class="container">
    <button @click="toggleForm" :class="{ 'white-button': showForm }">{{ showForm ? 'Close' : 'Add Task' }}</button>
    <div v-if="showForm" class="task-form">
      <div class="sub">
        <p>Task Name</p>
        <input type="text" v-model="taskName" placeholder="Task Name" class="input-field">
      </div>
      <div class="sub">
        <p>Time</p>
        <input type="text" v-model="taskTime" placeholder="Time" class="input-field">
      </div>
      <div class="sub">
        <p>Date</p>
        <input type="date" v-model="taskDate" placeholder="Date" class="input-field">
      </div>
      <button @click="submitTask" :disabled="isFormInvalid">Submit</button>
      <p v-if="isFormInvalid" class="error-message">Fill in all fields</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Button',
  data() {
    return {
      showForm: false,
      taskName: '',
      taskTime: '',
      taskDate: ''
    };
  },
  computed: {
    isFormInvalid() {
      return !this.taskName.trim() || !this.taskTime.trim() || !this.taskDate;
    }
  },
  methods: {
    toggleForm() {
      this.showForm = !this.showForm;
      if (!this.showForm) {
        this.clearFields();
      }
    },
    clearFields() {
      this.taskName = '';
      this.taskTime = '';
      this.taskDate = '';
    },
    submitTask() {
      const task = {
        name: this.taskName,
        time: this.taskTime,
        date: this.taskDate
      };
      this.$emit('task-submitted', task);
      this.clearFields();
      this.showForm = false;
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Julius+Sans+One&display=swap');

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
}

.white-button {
  font-family: "Julius Sans One", sans-serif;
  font-weight: 400;
  font-size: 18px;
  text-align: center;
  color: #000;
  border-radius: 20px;
  padding: 10px;
  width: 113px;
  height: 42px;
  background: #FFF;
}

button {
  font-family: "Julius Sans One", sans-serif;
  font-weight: 400;
  font-size: 18px;
  text-align: center;
  color: #fff;
  border-radius: 20px;
  padding: 10px;
  width: 113px;
  height: 42px;
  background: #000;
  margin-top: 20px;
}

.task-form {
  border: 1px solid #000;
  width: 230px;
  height: 330px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
}

.input-field {
  border: 1px solid #000;
  padding: 0px 0px 0px 5px;
  width: 190px;
  height: 20px;
  background: #fff;
}

p {
  font-family: "Julius Sans One", sans-serif;
  font-weight: 400;
  text-align: left;
  font-size: 16px;
  color: #000;
}
</style>
