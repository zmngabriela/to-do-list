<script setup>
  import { reactive } from "vue"
  import Head from './components/Head.vue'
  import Forms from './components/Forms.vue'
  import ToDo from "./components/ToDo.vue";

  const state = reactive({
    filter: 'all',
    tempTask: '',
    tasks: [
      {
        title: 'Study VueJS',
        concluded: false,
      },
      {
        title: 'Study React',
        concluded: false,
      },
      {
        title: 'Study Backend',
        concluded: true,
      },
    ]
  })

  const getPendingTasks = () => {
    return state.tasks.filter(tasks => !tasks.concluded)
  } 
  
  const getConcludedTasks = () => {
    return state.tasks.filter(tasks => tasks.concluded)
  }

  const getFilteredTasks = () => {
    const { filter } = state;

    switch (filter) {
      case 'pending':
        return getPendingTasks();
      case 'concluded':
        return getConcludedTasks();
      default:
        return state.tasks;
    }
  }

  const addTask = () => {
    const newTask = {
      title: state.tempTask,
      concluded: false,
    }
    state.tasks.push(newTask);
    state.tempTask = '';
  }
</script>

<template>
  <div class="container">
    <Head :pending-tasks="getPendingTasks().length"></Head>
    <Forms 
      :temp-task="state.tempTask" 
      :edit-temp-task="e => state.tempTask = e.target.value" 
      :add-task="addTask" 
      :change-filter="e => state.filter = e.target.value">
    </Forms>
    <ToDo :tasks="getFilteredTasks()"></ToDo>
  </div>
</template>
