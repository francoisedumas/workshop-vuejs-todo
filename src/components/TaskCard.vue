<template>
  <div :class="['task-card', { done }]">
    <div>
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
    </div>
    <Checkbox @click.native="$emit('toggle-task', taskIndex)" :checked="done" />
  </div>
</template>

<script>
import Checkbox from "./Checkbox";

export default {
  components: {
    Checkbox,
  },

  props: {
    title: String,
    description: String,
    done: Boolean,
    taskIndex: Number,
  },
};
</script>