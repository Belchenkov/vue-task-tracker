<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
        :color="showAddTask ? 'red' : 'green'"
        icon="fas fa-plus-circle"
        @btn-click="$emit('toggle-add-task')"
        :text="showAddTask ? 'Close' : 'Add Task'"
    />
    <Button
        text="Update Task"
        color="blue"
        icon="fas fa-edit"
    />
    <Button
        text="Delete Task"
        color="red"
        icon="fas fa-trash"
    />
  </header>
</template>

<script>
import Button from "@/components/Button";

export default {
  name: 'Header',
  props: {
    title: String,
    showAddTask: Boolean
  },
  components: {
    Button
  }
}
</script>

<style scoped>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
  }
</style>
