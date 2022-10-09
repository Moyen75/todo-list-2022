<template>
  <div :key="task.id" v-for="task in tasks">
    <SingleTask v-if="task"
      @delete-task="$emit('delete-task', task.id)"
      @show-reminder="$emit('show-reminder', task.id)"
      :singelTask="task"
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