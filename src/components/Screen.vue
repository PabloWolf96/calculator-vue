<template>
  <div class="container-screen">
    <div class="screen">
      <p class="calc">{{ calc }}</p>
      <p v-if="limit">limit reached</p>
      <p v-else>{{ input }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["input", "calc", "limit"],
};
</script>

<style></style>
