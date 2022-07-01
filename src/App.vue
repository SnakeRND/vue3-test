<template>

  <div class="app">

    <h1>Посты</h1>
    <div class="app_btns">
      <post-button
          @click="showModal"
      >
        Создать пост
      </post-button>
      <post-select
        v-model="selectedSort"
        :options="sortOptions"
      >

      </post-select>
    </div>
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
      selectedSort: '',
      sortOptions: [
        {value: 'title', name: 'По названию'},
        {value: 'description', name: 'По содержимому'},
      ]
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
        const response = await axios.get('https://my-json-server.typicode.com/typicode/demo/posts');
        this.posts = response.data;
        this.isPostsLoading = false;
      } catch (e) {
        alert('Ошибка')
      }
    },
  },
  mounted() {
    this.fetchPosts();
  },
  watch: {
    selectedSort(newValue) {
      this.posts.sort((post1, post2) => {
        return post1[newValue]?.localeCompare(post2[newValue]);
      })
    }

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

.app_btns {
  display: flex;
  justify-content: space-between;
  margin: 15px 0;
}
</style>
