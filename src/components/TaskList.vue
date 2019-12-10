<template>
  <main class="task-list">
    <h1>Vue Composition API Todo</h1>
    <div class="add">
      <input type="text" v-model="newTaskText" />
      <button type="button" v-on:click="addTask()">Add task</button>
    </div>
    <div class="list">
      <h2>To Do</h2>
      <task
        v-for="task in nonCompletedTasks"
        :key="task.id"
        :task="task"
        v-bind:done.sync="task.done"
      />
    </div>

    <div class="list">
      <h2>Done</h2>
      <task
        v-for="task in completedTasks"
        :key="task.id"
        :task="task"
        v-bind:done.sync="task.done"
      />
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
  computed,
} from '@vue/composition-api';
import TaskItem from 'Task.vue';
import { Task } from '../task';

export default createComponent({
  setup() {
    const { taskList, nonCompletedTasks, completedTasks } = useTaskList();
    const { newTaskText, addTask } = useAddTask(taskList);

    return {
      taskList,
      newTaskText,
      addTask,
      nonCompletedTasks,
      completedTasks,
    };
  },
});

/** Add the code needed to handle rendering a list of tasks */
function useTaskList() {
  // List of task's we're going to render. Use reactive() to make the reactivity deep.
  const taskList = ref<Task[]>([]);

  // Filter out the two lists based on the completed status
  const nonCompletedTasks = computed(() =>
    taskList.value.filter((task) => task.done === false)
  );
  const completedTasks = computed(() =>
    taskList.value.filter((task) => task.done === true)
  );

  return { taskList, nonCompletedTasks, completedTasks };
}

/** Adds the code needed to add tasks to the task list */
function useAddTask(taskList: Ref<Task[]>) {
  const newTaskText = ref(''); // Text for the input element

  function addTask() {
    // Generate a new id lazily
    const newId = Math.round(Math.random() * 100);
    // Add the new task and make sure to keep reactivity!
    taskList.value.push(
      reactive({ taskText: newTaskText.value, id: newId, done: false })
    );
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
