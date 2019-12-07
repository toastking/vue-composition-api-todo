<template>
  <main class="task-list">
    <h1>Vue Composition API Todo</h1>
    <div class="add">
      <input type="text" v-model="newTaskText" />
      <button type="button" v-on:click="addTask()">Add task</button>
    </div>
    <div class="list">
      <h2>Task List</h2>
      <task v-for="task in taskList" :key="task.id" :task="task" />
    </div>
  </main>
</template>

<script lang="ts">
import {
  createComponent,
  ref,
  Ref,
  reactive,
  watch,
} from '@vue/composition-api';
import TaskItem from 'Task.vue';
import { Task } from '../task';

export default createComponent({
  setup() {
    const { taskList } = useTaskList();
    const { newTaskText, addTask } = useAddTask(taskList);
    return { taskList, newTaskText, addTask };
  },
});

/** Add the code needed to handle rendering a list of tasks */
function useTaskList() {
  // List of task's we're going to render. Use reactive() to make the reactivity deep.
  const taskList = reactive<Task[]>([]);
  return { taskList };
}

/** Adds the code needed to add tasks to the task list */
function useAddTask(taskList: Task[]) {
  const newTaskText = ref(''); // Text for the input element

  function addTask() {
    // Generate a new id lazily
    const newId = Math.round(Math.random() * 100);
    // Add the new task
    taskList.push({ taskText: newTaskText.value, id: newId, done: false });
    // Clear the input
    newTaskText.value = '';
  }

  return { newTaskText, addTask };
}
</script>

<style scoped>
.task-list .add {
  display: flex;
  flex-direction: row;
  justify-content: center;
  padding: 1em;
}

.task-list .add button {
  margin-left: 1em;
}

.task-list .add input {
  margin-left: 0;
}
</style>
