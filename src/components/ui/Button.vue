<template>

  <button class="post_btn">
    <slot></slot>
  </button>

</template>

<script>
export default {
  name: "post-button"
}
</script>

<style scoped>
.post_btn {
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
}
</style>
