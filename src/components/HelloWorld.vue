<template>
  <div class="hello">
    <div class="main">
      <div class="top">
        <h1>My Tasks</h1>
        <AddTask
          @show-tasks="showTask"
          :title="showTaskForm ? 'Close' : 'Add Task'"
          :color="showTaskForm ? 'red' : 'green'"
        />
      </div>
      <div class="task-form">
        <AddTaskForm v-if="showTaskForm" @add-task="addTask" />
      </div>
      <div>
        <AllTasks
          @delete-task="deleteTask"
          @show-reminder="showReminder"
          :tasks="tasks"
        />
      </div>
    </div>
  </div>
</template>

<script>
import AllTasks from "./AllTasks.vue";
import AddTask from "./AddTask.vue";
import AddTaskForm from "./AddTaskForm.vue";
export default {
  name: "HelloWorld",
  components: {
    AddTask,
    AddTaskForm,
    AllTasks,
  },
  data() {
    return {
      tasks: [],
      showTaskForm: false,
    };
  },
  methods: {
    addTask(task) {
      this.tasks = [...this.tasks, task];
    },
    showTask() {
      this.showTaskForm = !this.showTaskForm;
    },
    async deleteTask(id) {
      const res = await fetch(`https://wild-pink-pleat.cyclic.app/api/v1/taskDelete/${id}`, {
        method: "DELETE",
      });
      res.status === 200
        ? ((this.tasks = this.tasks.filter((task) => task.id !== id)),
          this.$swal.fire("Good job!", "Task deleted successfully!", "success"))
        : this.$swal.fire("ooops!", "something error!", "error");
    },
    async showReminder(id) {
      const res = await fetch(`https://wild-pink-pleat.cyclic.app/api/v1/taskUpdate/${id}`, {
        method: "PUT"
      });
      res.status === 200
        ? ((this.tasks = this.tasks.map((task) =>
            task.id === id ? { ...task, reminder: !task.reminder } : task
          )),
          this.$swal.fire("Good job!", "Task updated successfully!", "success"))
        : this.$swal.fire("ooops!", "something error!", "error");
    },
  },
  async created() {
    const res = await fetch("https://wild-pink-pleat.cyclic.app/api/v1/tasks");
    const {tasks} = await res.json();
    this.tasks = tasks;
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  width: 100%;
}
.main {
  width: 600px;
  border: 2px solid rgba(128, 128, 128, 0.333);
  margin: 50px auto;
  padding: 5px 10px;
  background-color: #c6e5e1;
  border-radius: 3px;
}
.top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
