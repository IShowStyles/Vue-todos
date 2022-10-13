<template>
 <div v-if="posts.length > 0">
   <h2>
     Список Пользователей
   </h2>
   <transition-group name="post-list">
     <PostItem
         v-for="post in posts"
         :post="post"
         :key="post.id"
         @remove="$emit('remove',post)"
     />
   </transition-group>
 </div>
  <h3 v-else>
    List-Empty
  </h3>
</template>

<script>
import PostItem from "@/componets/PostItem"

export default {
  name : "post-list",
  components : {
    PostItem
  },
  props : {
    posts : {
      type : Array,
      required : true
    }
  }
}
</script>

<style scoped>
.post {
  padding: 5px;
  border: 2px solid teal;
  margin-top: 25px;
  width: 100%;
}


.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all .3s linear;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(-150px);
}

.post-list-move {
  transition: transform 0.5s ease-in-out;
}

</style>