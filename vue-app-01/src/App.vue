<template>
  <div class="container">
    <Header :showAddTask="showAddTask" title="Task tracker" @toggle-add-task="this.showAddTask = !this.showAddTask;"/>
    <AddTask @add-task="addTask" v-if="this.showAddTask"/>
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
      showAddTask: false
    }
  },
  methods: {
    deleteTask(id: string) {
      if(confirm('Are you shure you want to delete this task?')) {
        this.tasks = this.tasks.filter((task: any) => task.id !== id );
      }
    },
    toggleReminder(id: string) {
      // map lets you menipulate the list of objects and return it after.
      this.tasks = this.tasks.map((task: any) => task.id === id ? { ...task, reminder: !task.reminder } : task)
    },
    addTask(task: any) {
      this.tasks = [...this.tasks, task]
    },
   async fetchTasks() {
     const res = await fetch('http://localhost:5050/tasks');

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
