<template>
  <div>
    <form class="form" @submit.prevent>
      <h4>Создание поста</h4>
      <my-input
          v-model="post.title"
          @input="post.title= $event.target.value"
          placeholder="Название"/>
      <my-input
          v-model="post.body"
          @input="post.body= $event.target.value"
          placeholder="Содержимое"/>
      <my-button @click="addPost" type="submit">Создать</my-button>
    </form>
  </div>
</template>

<script>
import MyButton from "@/componets/UI/MyButton";
export default {
  name: "post-form",
  components: {MyButton},
  data() {
    return {
      post: {
        title: "",
        body: ""
      }
    }
  },
  methods: {
    addPost() {
      this.post.id = Date.now();
      this.$emit("create",this.post)
      this.post ={
        title: "",
        body: "",
      }
    }
  }
}
</script>

<style scoped>


.form {
  display: flex;
  flex-direction: column;
}

</style>