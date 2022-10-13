<template>
  <button class="btn">
      <slot></slot>
  </button>
</template>

<script>
export default {
  name: "my-button"
}
</script>

<style scoped>

.btn {
  outline: transparent;
  padding: 18px 12px;
  margin-top: 20px;
  align-self: flex-end;
  background: teal;
  color: aliceblue;
  border: transparent;
  text-transform: uppercase;
  border-radius: 15px;
}
</style>