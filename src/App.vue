<template>
  <div id="app">
    <task-list />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import TaskList from './components/TaskList.vue';
import TaskItem from './components/TaskItem.vue';

Vue.component('task-list', TaskList);
Vue.component('task', TaskItem);

export default Vue.extend({
  name: 'app',
  components: {},
});
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
