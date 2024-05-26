<template>
  <div class="taskslist">
    <div class="task" v-for="(task, index) in tasks" :key="index">
      <div class="note">
        <p>{{ task.name }}</p>
        <p>{{ task.time }}</p>
        <p>{{ task.date }}</p>
      </div>
      <div class="btn">
        <button @click="confirmDelete(index)" class="delete-button" :class="{ 'confirm': confirmIndex === index }">
          <svg width="15" height="14" viewBox="0 0 15 14" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M1.9 14L0.5 12.6L6.1 7L0.5 1.4L1.9 0L7.5 5.6L13.1 0L14.5 1.4L8.9 7L14.5 12.6L13.1 14L7.5 8.4L1.9 14Z" fill="black" />
          </svg>
        </button>
        <div v-if="confirmIndex === index" class="confirm-delete">
          <p>Are you sure you want to delete this task?</p>
          <button @click="deleteTask(index)">Yes</button>
          <button @click="cancelDelete">No</button>
        </div>
        <button @click="toggleIcon(task)" class="toggleIcon">
          <svg v-if="!task.showFirstIcon" width="30" height="30" viewBox="0 0 25 26">
            <path d="M12.5 25.5C10.7708 25.5 9.14583 25.1719 7.625 24.5156C6.10417 23.8594 4.78125 22.9688 3.65625 21.8438C2.53125 20.7188 1.64062 19.3958 0.984375 17.875C0.328125 16.3542 0 14.7292 0 13C0 11.2708 0.328125 9.64583 0.984375 8.125C1.64062 6.60417 2.53125 5.28125 3.65625 4.15625C4.78125 3.03125 6.10417 2.14062 7.625 1.48438C9.14583 0.828125 10.7708 0.5 12.5 0.5C14.2292 0.5 15.8542 0.828125 17.375 1.48438C18.8958 2.14062 20.2188 3.03125 21.3438 4.15625C22.4688 5.28125 23.3594 6.60417 24.0156 8.125C24.6719 9.64583 25 11.2708 25 13C25 14.7292 24.6719 16.3542 24.0156 17.875C23.3594 19.3958 22.4688 20.7188 21.3438 21.8438C20.2188 22.9688 18.8958 23.8594 17.375 24.5156C15.8542 25.1719 14.2292 25.5 12.5 25.5ZM12.5 23C15.2917 23 17.6562 22.0312 19.5938 20.0938C21.5312 18.1562 22.5 15.7917 22.5 13C22.5 10.2083 21.5312 7.84375 19.5938 5.90625C17.6562 3.96875 15.2917 3 12.5 3C9.70833 3 7.34375 3.96875 5.40625 5.90625C3.46875 7.84375 2.5 10.2083 2.5 13C2.5 15.7917 3.46875 18.1562 5.40625 20.0938C7.34375 22.0312 9.70833 23 12.5 23Z" fill="black" />
           
          </svg>
          <svg v-else width="30" height="30" viewBox="0 0 25 26">
             <path d="M10.75 18.75L19.5625 9.9375L17.8125 8.1875L10.75 15.25L7.1875 11.6875L5.4375 13.4375L10.75 18.75ZM12.5 25.5C10.7708 25.5 9.14583 25.1719 7.625 24.5156C6.10417 23.8594 4.78125 22.9688 3.65625 21.8438C2.53125 20.7188 1.64062 19.3958 0.984375 17.875C0.328125 16.3542 0 14.7292 0 13C0 11.2708 0.328125 9.64583 0.984375 8.125C1.64062 6.60417 2.53125 5.28125 3.65625 4.15625C4.78125 3.03125 6.10417 2.14062 7.625 1.48438C9.14583 0.828125 10.7708 0.5 12.5 0.5C14.2292 0.5 15.8542 0.828125 17.375 1.48438C18.8958 2.14062 20.2188 3.03125 21.3438 4.15625C22.4688 5.28125 23.3594 6.60417 24.0156 8.125C24.6719 9.64583 25 11.2708 25 13C25 14.7292 24.6719 16.3542 24.0156 17.875C23.3594 19.3958 22.4688 20.7188 21.3438 21.8438C20.2188 22.9688 18.8958 23.8594 17.375 24.5156C15.8542 25.1719 14.2292 25.5 12.5 25.5ZM12.5 23C15.2917 23 17.6562 22.0312 19.5938 20.0938C21.5312 18.1562 22.5 15.7917 22.5 13C22.5 10.2083 21.5312 7.84375 19.5938 5.90625C17.6562 3.96875 15.2917 3 12.5 3C9.70833 3 7.34375 3.96875 5.40625 5.90625C3.46875 7.84375 2.5 10.2083 2.5 13C2.5 15.7917 3.46875 18.1562 5.40625 20.0938C7.34375 22.0312 9.70833 23 12.5 23Z" fill="black" />
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskList',
  props: {
    tasks: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      confirmIndex: null
    };
  },
  methods: {
    confirmDelete(index) {
      this.confirmIndex = index;
    },
    deleteTask(index) {
      this.$emit('delete-task', index);
      this.confirmIndex = null; // Clear confirmIndex after deletion
    },
    cancelDelete() {
      this.confirmIndex = null;
    },
    toggleIcon(task) {
      // Зміна значення властивості showFirstIcon відповідного завдання
      task.showFirstIcon = !task.showFirstIcon;
    }
  }
}
</script>


<style scoped>
.taskslist {
  padding: 6px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.task {
  justify-content: space-between; /* Розподіляє елементи по краях контейнера */
  align-items: center;
  display: flex;
  flex-direction: row;
  position: relative;
  border: 2px solid #fff;
  padding: 10px;
  width: 249px;
  height: auto;
  background: linear-gradient(90deg, rgba(255, 255, 255, 0.61) 74.5%, rgba(255, 255, 255, 0.61) 100%);
  margin-bottom: 10px;
}

.note {
  width: 131px;
  font-family: "Julius Sans One", sans-serif;
  font-weight: 400;
  font-size: 16px;
}

.delete-button {
  border: none;
  background: none;
  cursor: pointer;
  position: absolute;
  top: 0%;
  right: 0%;
  margin: 5px;
}

.confirm-delete {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.confirm-delete p {
  margin-bottom: 10px;
  font-family: "Julius Sans One", sans-serif;
  font-weight: 400;
  font-size: 16px;
}

.confirm-delete button {
  margin-right: 10px;
  font-family: "Julius Sans One", sans-serif;
  font-weight: 400;
  font-size: 12px;
}

.toggleIcon {
  border: none;
  background: none;
  position: absolute;
  bottom: 0%;
  right: 0%;
}
</style>
