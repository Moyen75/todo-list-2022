<template>
  <div>
    <form @submit="onSubmit">
      <label for="Task">Add Task</label>
      <input type="text" name="task" placeholder="Add Task" v-model="task" />
      <label for="date">Add Date</label>
      <input type="text" name="date" placeholder="Add Date" v-model="date" />
      <label for="time">Add Time</label>
      <input type="text" name="time" placeholder="Add Time" v-model="time" />
      <div class="reminder">
        <label for="time">Set Reminder</label>
        <input type="checkbox" name="reminder" v-model="reminder" />
      </div>
      <input class="submit" type="submit" value="Submit" />
    </form>
  </div>
</template>
<script>
export default {
  name: "AddTaskForm",
  data() {
    return {
      task: "",
      date: "",
      time: "",
      reminder: false,
    };
  },
  methods: {
    async onSubmit(e) {
      e.preventDefault();
      const task = {
        id: Math.floor(Math.random() * 100000000000),
        task: this.task,
        date: this.date,
        time: this.time,
        reminder: this.reminder,
      };
      if (!this.task && !this.date && !this.time)
        return alert("something missing!");
      const res = await fetch("http://localhost:3000/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const data = await res.json();
      if (data) {
        this.$emit("add-task", data);
        this.$swal.fire("Good job!", "Task added successfully!", "success");
      }
      this.task = "";
      this.date = "";
      this.time = "";
      this.reminder = false;
    },
  },
};
</script>
<style scoped>
input {
  display: block;
  padding: 4px;
  border: gray;
  border-radius: 3px;
  width: 90%;
  margin: 6px auto;
}
label {
  margin-left: 9px;
  font-weight: 600;
}
.reminder {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
.reminder input {
  display: inline;
  width: 20%;
}
.submit {
  width: 92%;
  background-color: goldenrod;
  font-weight: 700;
  padding: 8px;
  color: white;
}
</style>