<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md todo-container">
      <!-- Header Section -->
      <div class="header-section">
        <h1 class="text-center">To-Do List</h1>
      </div>

      <!-- Input Section -->
      <div class="input-section">
        <q-input
          v-model="newTask"
          label="Add a task"
          outlined
          class="q-mb-sm"
          @keyup.enter="addTask"
        />
        <q-btn
          @click="addTask"
          label="Add Task"
          color="primary"
          class="full-width-btn"
        />
      </div>

      <!-- Task List Section -->
      <div class="task-list-section">
        <div class="q-row q-gutter-sm">
          <div
            v-for="(task, index) in tasks"
            :key="index"
            class="q-col-12 q-col-sm-6 q-col-md-4"
          >
            <q-card class="q-pa-sm task-card">
              <div class="task-content">
                <span>{{ task }}</span>
                <q-btn
                  @click="removeTask(index)"
                  icon="delete"
                  color="negative"
                  flat
                  class="remove-btn"
                />
              </div>
            </q-card>
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { ref } from "vue";

const newTask = ref("");
const tasks = ref([]);

// Add a task to the to-do list
function addTask() {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value.trim());
    newTask.value = "";
  }
}

// Remove a task from the list
function removeTask(index) {
  tasks.value.splice(index, 1);
}
</script>

<style scoped>
/* Main container */
.todo-container {
  max-width: 1200px;
  width: 100%;
  background-color: #f7f7f7;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
}

/* Header section */
.header-section {
  text-align: center;
  margin-bottom: 10px;
}

/* Input section */
.input-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

/* Button - full width */
.full-width-btn {
  width: 100%;
}

/* Task list responsiveness */
.task-card {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task-content {
  flex-grow: 1;
  padding: 10px;
  font-size: 16px;
}

/* Task delete button */
.remove-btn {
  cursor: pointer;
}
</style>
