<template>
  <div>
    <h1>To-Do List</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task">
    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index" :class="{ 'completed': task.completed }">
        <span @click="toggleTask(index)">{{ task.description }}</span>
        <button @click="deleteTask(index)">Delete</button>
      </li>
    </ul>
    <div class="filter">
      <label>Show only incomplete tasks:</label>
      <input type="checkbox" v-model="showOnlyIncomplete">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { description: 'Example task 1', completed: false },
        { description: 'Example task 2', completed: true }
      ],
      newTask: '',
      showOnlyIncomplete: false
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ description: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    }
  },
  computed: {
    filteredTasks() {
      if (this.showOnlyIncomplete) {
        return this.tasks.filter(task => !task.completed);
      } else {
        return this.tasks;
      }
    }
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
.filter {
  margin-top: 10px;
}
</style>
