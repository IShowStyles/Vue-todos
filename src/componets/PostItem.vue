<template>
  <div class="post">
    <div>
      <div><strong>Заголовок</strong> {{ post.title }}</div>
      <div><strong>Описание</strong> {{ post.body }}</div>
    </div>
    <my-button @click="$emit('remove',post)">
      DELETE
    </my-button>
  </div>
</template>

<script>
import MyButton from "@/componets/UI/MyButton";
export default {
  name: "PostItem",
  components: {MyButton},
  props : {
    post : {
      type : Object,
      required : true,
    }
  }
}
</script>

<style scoped>
  .post{
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
</style>