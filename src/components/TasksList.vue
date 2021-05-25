<template>
  <div id="tasks">
    <div v-if="tasks.length > 0" class="tasks-list">
      <button
        class="btn round-icon"
        v-on:click="newFormVisible = !newFormVisible">
            {{newFormVisible ? "x" : "+"}}
      </button>
      <NewTask v-if="newFormVisible" @add-task="addTask" />
      <TaskCard
        v-for="(task, index) in tasks"
        :key="index"
        :title="task.title"
        :description="task.description"
        :done="task.done"
      />
    </div>
    <p v-else-if="!newFormVisible">You don't have any tasks yet...</p>
  </div>
</template>

<script>
import TaskCard from './TaskCard.vue'
import NewTask from './NewTask.vue'

export default ({
  components: {
    TaskCard,
    NewTask
  },
  data() {
    return {
      tasks: [
        {
            title: "Create a card component",
            description:
            "Create a new TaskCard.vue file in the components folder, then import it in TasksList",
            done: false,
        },
        {
            title: "Make the card component dynamic",
            description:
            "Learn about using the data option and passing data to child components using props",
            done: true,
        },
        {
            title: "Bind the attributes to the data",
            description:
            "Use the v-bind directive to bind the title and description to our data",
            done: false,
        },
      ],
      newTitle: "",
      newDescription: "",
      newFormVisible: false,
    };
  },
  methods: {
    addTask(title, description, done = false) {
        this.tasks.unshift({ title, description, done });
        this.newFormVisible = false;
    },
    resetForm(){
        this.newDescription = ""
        this.newTitle = ""
    },
    toggleTask(taskIndex) {
      const taskToUpdate = this.tasks[taskIndex];
      taskToUpdate.done = !taskToUpdate.done;
      this.$set(this.tasks, taskIndex, taskToUpdate);
    },
  }
})
</script>

<!-- TaskCard.vue -->

<style lang="scss">
.task-card {
  display: flex;
  min-height: 6rem;
  text-align: left;
  background-color: saturate(rgba(#41b883, 0.03), 30%);
  border-bottom: solid 1px rgba(#35495e, 0.1);
  border-left: solid 8px #41b883;
  transition: all 0.3s;
  p { font-size: 0.9rem; }
  &:hover {
    transform: scale(1.02);
    background-color: white;
    box-shadow: 2px 3px 10px rgba(black, 0.1);
  }
  & > div:first-child {
    margin: 0 1rem;
    padding: 1rem 0;
    display: flex;
    flex-grow: 1;
    flex-direction: column;
    justify-content: center;
  }
  &.done {
    border-left: solid 8px rgba(#35495e, 0.3);
    background-color: rgba(#35495e, 0.08);
    h3, p { text-decoration: line-through; opacity: 0.3; }
    &:hover { transform: unset; box-shadow: unset; }
  }
}
@keyframes expand-vertical { from { min-height: 0; height: 0; } to { min-height: 6rem; } }
.task-card.new-task {
  animation: expand-vertical 0.2s;
  overflow: hidden;
  background-color: white;
  border-left: solid 5px #35495e;
  &, &:hover { transform: scale(1.1); box-shadow: 2px 3px 10px rgba(black, 0.2); }
  & + .tasks-list { pointer-events: none; }
  input { font-size: 1.17rem; font-weight: bold; width: 100%; }
  textarea { width: 100%; font-size: 0.9rem; resize: none; }
}
</style>
