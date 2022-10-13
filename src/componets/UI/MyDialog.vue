<template>
  <div class="dialog" v-if="show" @click.stop="hideDialog">
      <div @click.stop class="dialog-content">
        <slot></slot>
      </div>
  </div>
</template>

<script>
export default {
  name: "my-dialog",

  props: {
    show: {
      type: Boolean,
      default: true
    }
  },
  methods : {
    hideDialog(){
      this.$emit("update:show",false)
    }
  }

}
</script>

<style scoped>
  .dialog{
    position: fixed;
    display: flex;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(0,0,0,0.6);
  }

  .dialog-content{
    padding: 20px;
    background-color: white;
    margin: auto;
    border-radius : 20px;
    min-height: 50px;
    min-width: 300px;
  }

</style>