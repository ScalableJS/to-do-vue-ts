<template>
  <form @submit.prevent="handlerSubmit">
    <label for="newItem">Add to the todo list</label>
    <input id="newItem" type="text" v-model="taskName" />
    <button>Add</button>
  </form>
</template>

<script lang="ts">
import type { Task } from "../types/Task";

const generateId = () => {
  return Math.random().toString(36).substring(2);
};

export default {
  name: "NewTask",
  data() {
    return {
      taskName: "",
    };
  },
  methods: {
    handlerSubmit() {
      this.$emit("add", {
        id: generateId(),
        name: this.taskName,
        isDone: false,
      } as Task);
    },
  },
};
</script>
<style scoped></style>
