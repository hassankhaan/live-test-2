<script setup>
import { ref } from "vue";

const tasks = ref([
  { name: "Task 1", time: "30" },
  { name: "Task 2", time: "40" },
  { name: "Task 3", time: "60" },
  { name: "Task 4", time: "45" },
  { name: "Task 5", time: "50" },
]);

const isEdit = ref(false);
const editId = ref(2);
const taskName = ref('');
const taskTime = ref('');

const updateTask = (id) => {
  tasks.value[id].name = taskName.value;
  tasks.value[id].time = taskTime.value;
  isEdit.value = false;
}

const editTask = (index) => {
  editId.value = index;
  taskName.value = tasks.value[index].name;
  taskTime.value = tasks.value[index].time;
  isEdit.value = true;
}
</script>

<template>
  <div class="flex items-center justify-center min-h-screen">
    <div class="max-w-3xl mx-5 w-full p-6 rounded-xl shadow-xl bg-teal-500">
      <h1 class="text-3xl font-bold text-center text-white">Tasks List</h1>
      <div
        v-for="(task, index) in tasks"
        :key="index"
        class="flex items-center border-b-2 py-2 bg-white p-5 rounded-lg my-3"
      >
        <span class="text-md font-bold">{{ task.name }} - {{ task.time }} minutes</span>
        <div class="flex justify-end items-center flex-grow">
          <button @click="editTask(index)" class="bg-blue-600 p-3 rounded-xl font-bold text-white mr-2">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-4 h-4"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L10.582 16.07a4.5 4.5 0 0 1-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 0 1 1.13-1.897l8.932-8.931Zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0 1 15.75 21H5.25A2.25 2.25 0 0 1 3 18.75V8.25A2.25 2.25 0 0 1 5.25 6H10"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>
  </div>
  
  <div v-if="isEdit" class="fixed top-0 left-0 w-full h-full flex items-center justify-center">
    <div class="absolute top-0 left-0 w-full h-full bg-gray-900 opacity-50"></div>
    <div class="z-10 lg:w-1/3 md:w-1/2 sm:w-1/2 w-full mx-5 max-w-3xl p-4 bg-white rounded-md">
      <div class="my-1 p-2 bg-red-500 text-white rounded-md" v-if="showAlert">
        Please fill in all required fields.
      </div>
      <button @click="isEdit = false" class="absolute top-0 right-0 p-4">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
          <path stroke-linecap="round" stroke-linejoin="round" d="m9.75 9.75 4.5 4.5m0-4.5-4.5 4.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
        </svg>

      </button>
      <h2 class="text-2xl font-bold mb-4">Edit Task</h2>
      <div class="mb-4">
        <label class="block text-sm font-medium text-gray-700">Task Name</label>
        <input type="text" required v-model="taskName" class="mt-1 p-2 w-full border rounded-md">
      </div>
      <div class="mb-4">
        <label class="block text-sm font-medium text-gray-700">Task Time (minutes)</label>
        <input type="number" required v-model="taskTime" @keypress.enter="updateTask(editId)" class="mt-1 p-2 w-full border rounded-md">
      </div>
      <button @click="updateTask(editId)" class="bg-black w-full text-white p-3 font-bold rounded-xl">Update Task</button>
    </div>
  </div>
</template>
