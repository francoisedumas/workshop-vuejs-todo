<template>
  <div :class="['task-card', { done }]">
    <div>
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
    </div>
    <div>{{ done ? "✅" : "⭕️" }}</div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    description: String,
    done: { type: Boolean, default: false }
  },
};
</script>