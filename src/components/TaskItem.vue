<template>
  <div class="task-item">
    <input type="checkbox" id="task-checkbox" v-model="isCompleted" />
    <p>{{ task.taskText }}</p>
  </div>
</template>

<script lang="ts">
import {
  createComponent,
  SetupContext,
  ref,
  watch,
} from '@vue/composition-api';
import { Task } from '../task';

export default createComponent({
  props: { task: Object },
  setup(props: { task: Task }, context) {
    const { isCompleted } = useTaskCompletion(context, props.task.done);
    return { isCompleted };
  },
});

/** Setup the task completion code */
function useTaskCompletion(context: SetupContext, initialValue: boolean) {
  const isCompleted = ref(initialValue);

  watch(() => {
    // Emit an event to the parent component when the complete value changes
    context.emit('update:done', isCompleted.value);
  });
  return { isCompleted };
}
</script>

<style scoped>
.task-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 0.5em;
  border-bottom: 1px solid #cccccc;
}

.task-item input {
  margin-left: 1em;
}
</style>
