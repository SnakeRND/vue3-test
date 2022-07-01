<template>

  <div class="app">

    <h1>Посты</h1>
    <post-button
        @click="showModal"
        style="margin: 15px 0;"
    >
      Создать пост
    </post-button>
    <post-modal v-model:show="modalVisible">
      <post-form
          @create="createPost"
      />
    </post-modal>
    <post-list
        :posts="posts"
        @remove="removePost"
        v-if="!isPostsLoading"
    />
    <div v-else>Идет загрузка...</div>

  </div>

</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    PostForm, PostList
  },
  data() {
    return {
      posts: [],
      modalVisible: false,
      isPostsLoading: false,
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.modalVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showModal() {
      this.modalVisible = true;
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        setTimeout(async () => {
          const response = await axios.get('https://my-json-server.typicode.com/typicode/demo/posts');
          this.posts = response.data;
          this.isPostsLoading = false;
        }, 1000)
      } catch (e) {
        alert('Ошибка')
      }
    },
  },
  mounted() {
    this.fetchPosts();
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}
</style>
