<template>
  <main>
    <header>
      <h1>Pinia tasks </h1>
    </header>

    <div class="new-task-form">
      <TaskForm />
    </div>
    <nav class="filter">
      <button @click="filter = 'all'" >All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <div class="task-list" v-if="filter === 'all' ">
      <p>You have {{ taskStore.totalCount}} tasks left to do </p>
      <div v-for="task in taskStore.tasks" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs' ">
      <p>You have {{ taskStore.favCount}} favs left to do </p>
      <div v-for="task in taskStore.favs" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from 'vue';
import TaskDetails from './components/TaskDetail.vue';
import TaskForm from './components/TaskForm.vue'; // Corrected import
import { useTaskStore } from './stores/TaskStore';

export default {
  components: { TaskDetails, TaskForm }, // Corrected component name
  setup() {
    const taskStore = useTaskStore();
    const filter = ref('all');

    return { taskStore, filter };
  },
};
</script>

