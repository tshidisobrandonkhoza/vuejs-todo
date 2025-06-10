<!-- copositionwe have setup function -->

<script setup>
// make data reactive with ref
import { onMounted, ref } from 'vue';

const title = ref('To Do');
const status = ref(false);
const tasks = ref([]);
let message = ref('Not Active');
const newTask = ref('');
const toggleStatus = () => {
  if (!status.value) {
    message.value = 'User Has No  ist';
  } else {
    message.value = 'User List Active';
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

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {

  }
});
</script>

<template>
  <div class="m-5">
    <h1 class="text-2xl font-semibold ">{{ title }}</h1>
    <p class="status">{{ message }}</p>
  </div>
  <!-- can prevent the default directly -->
  <form @submit.prevent="addTask">
    <label for="newTask"></label>
    <!-- binding -->
    <input type="text" id="newTask" name="newTask" placeholder="Add New Task" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <button class="add-btn" @click="toggleStatus" v-if="tasks.length > 0">
    {{ !status ? 'Hide Task' : 'Show Task' }}
  </button>
  <ul v-if="!status">
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ index + 1 }} | {{ task }}  </span>
      <button class="btn-remove" @click="removeTask(index)"> remove</button>
    </li>
  </ul>
</template>

<style scoped>
.status {
  background-color: rgb(75, 75, 75);
  border-radius: .3em;
  padding: .2em .4em;
  width: 8em;
  color: #ffffff;
  text-align: center;
}

form {
  margin: .2em;
  background-color: rgb(75, 75, 75);
  border-radius: .3em;
  padding: .2em .4em;
  color: #fff;
  width: calc(100% - 5em);
  margin: 1em;
}

.add-btn {
  width: calc(100% - 5em);
  margin: 1em;
  background-color: rgb(43, 0, 255);
  border-radius: .3em;
  padding: .2em .4em;
  color: #fff;
}

ul {
  margin: 1em;
  display: flex;
  flex-direction: column;
  gap: .3em;
  width: calc(100% - 5em);
}

ul li {
  margin: .2em;
  background-color: rgb(75, 75, 75);
  border-radius: .3em;
  padding: .2em .4em;
  color: #fff;
}

.btn-remove {

  background-color: red;
  border-radius: .3em;
  padding: .2em .4em;
}
</style>