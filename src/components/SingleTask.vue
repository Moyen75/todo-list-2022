<template>
  <div class="task" @dblclick="$emit('show-reminder', task.id)">
    <h1>
      {{ task.task }}
      <i v-if="task.task" @click="onDelete(task.id)" class="fa-solid fa-trash-can"></i>
    </h1>
    <div class="reminder">
      <h3>{{ task.date }}</h3>
      <h3>{{ task.time }}</h3>
      <i :class="[task.reminder ? 'fa-solid fa-bell' : '']"></i>
    </div>
  </div>
</template>
<script>
export default {
  name: "SingleTask",
  props: {
    task: Object,
  },
  methods: {
    onDelete(id) {
      this.$emit("delete-task", id);
    },
  },
};
</script>
<style scoped>
.task {
  border: 1px solid yellow;
  background: rgba(173, 172, 172, 0.493);
  width: 90%;
  margin: 5px auto;
  border-radius: 3px;
  padding: 20px;
}
.fa-bell{
  cursor: pointer;
}
.fa-trash-can {
  color: red;
  font-size: 25px;
  cursor: pointer;
}
.reminder {
  display: flex;
  align-items: center;
  justify-content: space-between;
  line-height: 0;
  margin: 0;
}
h1 {
  display: flex;
  justify-content: space-between;
  text-transform: capitalize;
  line-height: 0;
}
</style>