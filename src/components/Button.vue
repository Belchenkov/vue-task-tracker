<template>
  <button
      @click="onClick"
      class="btn"
      :style="{ background: color }"
  >
    <i class="mr-2" :class="icon"></i>
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    color: String,
    icon: String,
  },
  methods: {
    onClick() {

    }
  }
}
</script>

<style scoped>

</style>