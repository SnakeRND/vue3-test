<template>

  <div class="app">
    <post-form
        @create="createPost"
    />
    <post-list
        :posts="posts"
    />
  </div>

</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
export default {
  name: "App",
  components: {
    PostForm, PostList
  },
  data() {
    return {
      posts: [
        {id: 1, title: 'Пост 1', description: 'Описание 1.'},
        {id: 2, title: 'Пост 2', description: 'Описание 2.'},
        {id: 3, title: 'Пост 3', description: 'Описание 3.'},
        {id: 4, title: 'Пост 4', description: 'Описание 4.'},
        {id: 5, title: 'Пост 5', description: 'Описание 5.'},
      ],
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
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
</style>
