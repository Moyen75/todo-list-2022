<template>
  <div :key="task.id" v-for="task of tasks">
    <SingleTask
      @delete-task="$emit('delete-task', task.id)"
      @show-reminder="$emit('show-reminder', task.id)"
      :task="task"
    />
  </div>
</template>
<script>
import SingleTask from "./SingleTask.vue";
export default {
  name: "AllTasks",
  props: {
    tasks: Array,
  },
  components: {
    SingleTask,
  },
  emits: ["delete-task", "show-reminder"],
};
</script>