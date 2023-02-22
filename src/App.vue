<template>
  <h1>Todo List</h1>
  <span>Get things done, one item at a time.</span>
  <NewTask @add="handlerAddNewTask" />
  <div>
    <div v-for="(task, i) in tasks" :key="i">
      <TaskItem :task="task" @delete="handlerDelete" @change="handlerChange" />
    </div>
  </div>
</template>

<script lang="ts">
import NewTask from "./components/NewTask.vue";
import TaskItem from "./components/TaskItem.vue";
import type { Task } from "./types/Task";

const tasks: Task[] = [
  {
    id: "1",
    name: "123",
    isDone: true,
  },
];

export default {
  name: "App",
  components: { TaskItem, NewTask },
  data() {
    return {
      tasks: tasks,
      newTaskName: "",
    };
  },
  methods: {
    handlerAddNewTask(task: Task) {
      this.tasks.push(task);
    },
    handlerChange(data: { id: string; isDone: boolean }) {
      const task = this.tasks.find((item) => item.id === data.id) as Task;
      task.isDone = data.isDone;
    },
    handlerDelete(id: string) {
      this.tasks = this.tasks.filter((item) => item.id !== id);
    },
  },
};
</script>

<style scoped></style>
