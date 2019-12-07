<template>
  <div class="task-item">{{ task.taskText }}</div>
</template>

<script lang="ts">
import { createComponent } from '@vue/composition-api';
import { Task } from '../task';

export default createComponent({
  props: { task: Object },
});
</script>

<style scoped>
.task-item {
  display: flex;
  flex-direction: row;
  padding: 0.5em;
  border-bottom: 1px solid #cccccc;
}
</style>
