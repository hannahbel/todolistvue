<template>
  <div class="container">
    <div class="task">
    
      <div class="title">
        <h1> To Do List!</h1>
        <h4>It's always time for productivity.</h4>
      </div>
     
      <div class="form">
        <input
          type="text"
          placeholder="New Task"
          v-model="newTask"
          @keyup.enter="addTask"
        />
        <button @click="addTask"><i class="fas fa-plus"></i></button>
      </div>

      <div class="taskItems">
        <ul>
          <task-item
            v-bind:task="task"
            v-for="(task, index) in tasks"
            :key="task.id"
            @remove="removeTask(index)"
            @complete="completeTask(task)"
          ></task-item>
        </ul>
      </div>
    
      <div class="clearBtns">
        <button @click="clearCompleted">Clear completed</button>
        <button @click="clearAll">Clear all</button>
      </div>
     
      <div class="pendingTasks">
        <span>Pending Tasks: {{ incomplete }}</span><span>ㅤㅤㅤㅤㅤㅤ</span> <!--Tasks that are not marked/clicked as completed shall add up to this count-->
        <span>Completed Tasks: {{ complete }}</span> <!--Tasks that are marked/clicked as completed shall add up to this count-->
      </div>
    </div>
  </div>
</template>

<script>
import TaskItem from "./Task-item";

//BELOW IS THE BACKEND
export default {
  name: "Task",
  props: ['tasks'],
  components: {
    TaskItem,
  },
  data() {
    return {
      newTask: "",
    };
  },
  computed: {
    incomplete() {
      return this.tasks.filter(this.inProgress).length;
    },
    complete() {
      return this.tasks.filter(this.Progressed).length;
    },
  },
  methods: {
    addTask() {
      if (this.newTask) {
        this.tasks.push({
          title: this.newTask,
          completed: false,
        });
        this.newTask = "";
      }
    },
    inProgress(task) {
      return !this.isCompleted(task);
    },
    Progressed(task) {
      return this.isCompleted(task);
    },
    isCompleted(task) {
      return task.completed;
    },
    clearCompleted() {
      this.tasks = this.tasks.filter(this.inProgress);
    },
    clearAll() {
      this.tasks = [];
    },
    completeTask(task) {
      task.completed = !task.completed;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>
