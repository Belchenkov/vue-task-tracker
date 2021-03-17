<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
        v-show="homePage"
        :color="showAddTask ? 'red' : 'green'"
        icon="fas fa-plus-circle"
        @btn-click="$emit('toggle-add-task')"
        :text="showAddTask ? 'Close' : 'Add Task'"
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
  },
  computed: {
    homePage() {
      return this.$route.path === '/';
    }
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
