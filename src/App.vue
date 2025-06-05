<!-- copositionwe have setup function -->

<script setup>
// make data reactive with ref
import { ref } from 'vue';

const title = ref('To Do');
const status = ref(false);
const tasks = ref(['Task A', 'Task B', 'Task C', 'Task D']);
let message = ref('Not Active');
const newTask = ref('');
const toggleStatus = () => {
  if (!status.value) {
    message.value = 'User Not Active';
  } else {
    message.value = 'User Active';
  }
  status.value = !status.value;
}

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value)
    newTask.value = '';
  }

}
  const removeTask = (ind) => {

    tasks.value.splice(ind, 1);

  }
</script>

<template>
  <h1>{{ title }}</h1>
  <p>{{ message }}</p>
  <!-- can prevent the default directly -->
  <form @submit.prevent="addTask">
    <label for="newTask"></label>
    <!-- binding -->
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <button @click="toggleStatus" v-if="tasks.length > 0">
    {{ !status? 'Hide Task':'Show Task' }}
  </button>
  <ul v-if="!status">
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ index }}  | {{ task }} -  </span>
      <button @click="removeTask(index)"> remove</button>
    </li>
  </ul>
</template>