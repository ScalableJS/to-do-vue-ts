<template>
  <div class="task-item">
    <input
      class="task-item__status"
      type="checkbox"
      :id="taskUniqueStatusId"
      :checked="task.isDone"
      @change="changeStatus"
    />
    <label class="task-item__name" :for="taskUniqueStatusId">{{
      task.name
    }}</label>
    <button class="task-item__delete" @click="deleteTask">&times;</button>
  </div>
</template>
<script lang="ts">
import type { Task } from "../types/Task";

export default {
  name: "TaskItem",
  computed: {
    taskUniqueStatusId() {
      return "done" + this.task.id;
    },
  },
  props: {
    task: Object as Task,
  },
  methods: {
    deleteTask() {
      this.$emit("delete", this.task.id);
    },
    changeStatus() {
      this.$emit("change", {
        id: this.task.id,
        isDone: !this.task.isDone,
      });
    },
  },
};
</script>
<style scoped>
.task-item {
  display: flex;
  border: 1px solid #ccc;
  padding: 10px;
}
.task-item__name {
  order: -1;
  flex-grow: 1;
}
.task-item__status:checked + .task-item__name {
  text-decoration: line-through;
}
</style>
