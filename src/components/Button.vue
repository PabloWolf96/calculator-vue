<template>
  <button class="btn" :style="styles" @click="handleClick">
    {{ btn }}
  </button>
</template>

<script>
export default {
  props: ["btn", "styles"],
  methods: {
    handleClick(e) {
      this.$emit("clicked", e.target.textContent);
    },
  },
};
</script>

<style></style>
