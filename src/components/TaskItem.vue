<template>
  <div>{{ task.taskText }}</div>
</template>

<script lang="ts">
import { createComponent } from '@vue/composition-api';
import { Task } from '../task';

export default createComponent({
  props: { task: Object },
});
</script>
