<template>
  <input
      class="input"
      type="text"
     >
</template>

<script>
export default {
  name: "my-input",
  props : {
    modelValue : [String,Number]
  },
  methods : {
    updateInput (e){
      this.$emit("update:modelValue",e.target.value);
    }
  }
}
</script>

<style scoped>
.input {
  width: 100%;
  height: 38px;
  border: 1px solid #212121;
  margin-top: 15px;
}

.input::placeholder {
  padding-left: 17px;
}
</style>