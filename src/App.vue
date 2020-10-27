<template>
  <div id="app" class="container">
    <ListTasks :tasks="tasks" />
  </div>
</template>

<script>

import ListTasks from "./components/ListTasks"

export default {
  name: 'app',
  data() {
    return {
      tasks: [

      ],

    }
  },
  components: {
    ListTasks
  }
}
</script>

<style>

</style>
