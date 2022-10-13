<template>
  <div class="app">
    <h1>
      Страница с постами
    </h1>
    <my-input v-model="searchQuery">

    </my-input>
    <div class="app_btns">
      <my-button @click="showDialog" style="margin-right: 15px">
        Создать пост
      </my-button>
      <my-select v-model="selectSort" :options="sortOption"></my-select>
    </div>
    <my-dialog v-model:show="dialogVisible">
      <PostForm
          @create="addPost"/>
    </my-dialog>
    <PostList
        :posts="posts"
        @remove="removePost"
        v-if="isPostLoading"
    />
    <div v-else class="spinner">
      идет загрузка !!!
    </div>
  </div>
</template>

<script>
import PostForm from "@/componets/PostForm";
import PostList from "@/componets/PostList";
import axios from "axios";


export default {
  components: {
    PostForm, PostList
  },
  name: "App",
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostLoading: false,
      selectSort: "",
      searchQuery: "",
      sortOption: [
        {value: 'title', name: "по названию"},
        {value: 'body', name: "по описанию"},
      ]
    }
  },
  mounted() {
    this.fetchPosts();
  },
  methods: {
    addPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts() {
      try {
        setTimeout(async () => {
          this.isPostLoading = true;
          const response = await axios.get("https://jsonplaceholder.typicode.com/posts?_limit=10");
          this.posts = response.data;
          console.log(response)
        }, 1000)
      } catch (e) {
        console.log(e, +"err type")
      } finally {
        this.isPostLoading = false;
      }
    },
  },
  watch: {
    selectSort(newVal) {
      this.posts.sort((posts1,posts2)=>{
        return posts1[newVal]?.localeCompare(posts2[newVal])
      })
    }
  },
  computed : {
    searchAndSortedPost(){
      return this.selectSort.filter(post=> post.title.include(this.searchQuery))
    }
  }
}

</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}


#app {
  max-width: 1230px;
  margin: 0 auto;
}

.app_btns {
  display: flex;
  align-items: center;
  justify-content: space-between;

}


.app {
  padding: 20px;
}

</style>