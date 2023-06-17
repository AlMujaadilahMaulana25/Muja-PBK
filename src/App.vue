<template>
  <main class="content">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav>
    <router-view/>
    <header class="judul">
      <h1>Ampera Pangek Situjuah </h1>
    </header>

    <div class="new-task-form">
      <TaskForm/>
    </div>

    <nav class="filter">
      <button @click="filter = 'all'">Semua</button>
      <button @click="filter = 'favs'">Kesukaan</button>
    </nav>
    
    <div class="task-list" v-if="filter === 'all'">
      <p>Kamu mempunyai {{ taskStore.tasks.length }} Belanjaan </p>
      <div v-for="task in taskStore.tasks" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>Kamu mempunyai {{ taskStore.favs.length }} belanja kesukaan</p>
      <div v-for="task in taskStore.favs" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from 'vue';
import TaskDetails from './components/TaskDetails.vue';
import TaskForm from './components/TaskForm.vue';
import { useTaskStore } from './stores/TaskStore';

export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskStore();
    const filter = ref('all');

    return { taskStore, filter };
  },
};
</script>

<style>
.content {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 20px;
  background-color:  yellow;
}

.judul {
  background-color: greenyellow;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  text-decoration: none;
  margin-right: 10px;
}

nav a.router-link-exact-active {
  color: #42b983;
}

header {
  background-color: #f8f8f8;
  padding: 20px;
  margin-bottom: 30px;
  font-family: 'Times New Roman', Times, serif;
  font-weight: bold;
}

h1 {
  font-size: 35px;
  margin: 0;
}

.filter {
  padding: 10px;
  background-color: greenyellow;
  margin-bottom: 20px;
  display: flex;
  justify-content: center;
}

.filter button {
  padding: 8px 16px;
  margin-right: 10px;
  background-color: orange;
  color: #fff;
  border: none;
  cursor: pointer;
  border-radius: 20px;
  transition: background-color 0.3s ease;
}

.filter button:hover {
  background-color: orange;
}

.task-list {
  margin-top: 20px;
}

.task-list p {
  font-weight: bold;
  font-size: 18px;
  margin-bottom: 10px;
}

.task-list div {
  border: 1px solid #ddd;
  padding: 10px;
  margin-bottom: 10px;
  background-color: greenyellow;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.task-list div:hover {
  background-color: greenyellow;
}
</style>
