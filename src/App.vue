<!-- options must export default with scripst -->

<script>
export default {
  data() {
    return {
      title: 'To Do',
      status: true,
      tasks: ['Task A', 'Task B', 'Task C']
    };
  },
}
</script>

<template>
  <h1>{{ title }}</h1>
  <p v-if="status">User Active</p>
  <p v-if="!status">User Not Active</p>
  <button>Show Task</button>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">{{ task }} - {{ index }}</li>
  </ul>
</template>