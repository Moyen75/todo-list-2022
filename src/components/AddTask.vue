<template>
  <button :style="{ background: color }" @click="onClick()">{{ title }}</button>
</template>
<script>
export default {
  name: "AddTask",
  props: ["title", "color"],
  methods: {
    onClick() {
      this.$emit("show-tasks");
    },
  },
};
</script>
<style scoped>
button {
  background-color: green;
  color: white;
  padding: 8px;
  border: none;
  font-weight: 600;
  border-radius: 5px;
  cursor:pointer
}
</style>