<template>
  <div id="app">
    <task v-bind:tasks="tasks"></task>
  </div>
</template>

<script>
import Task from "./components/Task";

export default {
  name: "App",
  components: {
    Task,
  },
  data() {
    return {
      tasks: [ //To Do List tasks for temporary display
        {
          id: 1,
          title: "Create wireframe for EverMart website",
          completed: true,
        },
        {
          id: 2,
          title: "Finish revisions from client",
          completed: true,
        },
        {
          id: 3,
          title: "Update prices on toy listings",
          completed: false,
        },
        {
          id: 4,
          title: "Consult supervisor about reports",
          completed: false,
        },
        {
          id: 5,
          title: "Book an appointment at NBI",
          completed: false,
        },
      ],
    };
  },
};
</script>