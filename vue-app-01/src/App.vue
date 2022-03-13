<template>
  <div class="container">
    <Header :showAddTask="showAddTask" title="Task tracker" @toggle-add-task="this.showAddTask = !this.showAddTask;"/>
    <AddTask @add-task="addTask" v-if="this.showAddTask" :isLoading="this.isLoading"/>
    <TaskList @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks"/>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import Header from "./components/layout-header.vue";
import Task from "./components/element-task.vue";
import TaskList from './components/element-task-list.vue';
import AddTask from './components/add-task.vue';

@Options({
  name: 'app',
  components: {
    Header,
    Task,
    TaskList,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
      isLoading: false
    }
  },
  methods: {
    async deleteTask(id: string) {
      const res = await fetch(`api/tasks/${id}`, { method: 'DELETE' });

      res.status === 200 ? (this.tasks = this.tasks.filter((task: any) => task.id !== id )) : alert('Failed to delete item')
    },
    async toggleReminder(id: string) {
      const taskToToggle = await this.fetchTask(id);      
      taskToToggle.reminder = !taskToToggle.reminder;
      
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(taskToToggle)
      })
      // map lets you menipulate the list of objects and return it after.
      this.tasks = this.tasks.map((task: any) => task.id === id ? { ...task, reminder: !task.reminder } : task)
    },
    async addTask(task: any) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task),
      })

      const data = await res.json();

      this.tasks = [...this.tasks, data]
    },
    async fetchTasks() {
      const res = await fetch('api/tasks');

      const data = await res.json();

      return data;
    },
    async fetchTask(id: any) {
      const res = await fetch(`api/tasks/${id}`);

      const data = await res.json();

      return data;
    }
  },
  async created() {
    this.tasks = await this.fetchTasks();
  }
})
export default class App extends Vue {}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
