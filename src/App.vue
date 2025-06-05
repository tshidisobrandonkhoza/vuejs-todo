<!-- copositionwe have setup function -->

<script>
// make data reactive with ref
import { ref } from 'vue';

export default {
  setup() {
    const name = ref('To Do');
    const status = ref(false);
    const tasks = ref(['Task A', 'Task B', 'Task C', 'Task D']);
    let message = ref('Not Active');
    const toggleStatus = () => {
      if (!status.value) {
        message.value = 'User Not Active';
      } else {
        message.value = 'User Active';
      }
      status.value = !status.value;
    }

    return {
      name,
      status,
        tasks,
      message,
      toggleStatus
    }
  },
};
</script>

<template>
  <h1>{{ title }}</h1>
  <p>{{ message }}</p>
  <button @click="toggleStatus">Show Task</button>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">{{ task }} - {{ index }}</li>
  </ul>
</template>