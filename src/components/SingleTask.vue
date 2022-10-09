<template>
  <div class="task" @dblclick="$emit('show-reminder', singelTask.id)">
    <h1>
      {{ singelTask?.task }}
      <i v-if="singelTask.task" @click="onDelete(singelTask.id)" class="fa-solid fa-trash-can"></i>
    </h1>
    <div class="reminder">
      <h3>{{ singelTask.date }}</h3>
      <h3>{{ singelTask.time }}</h3>
      <i :class="[singelTask.reminder ? 'fa-solid fa-bell' : '']"></i>
    </div>
  </div>
</template>
<script>
export default {
  name: "SingleTask",
  props: {
    singelTask: Object,
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