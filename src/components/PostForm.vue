<template>

  <form @submit.prevent>
    <h4>Создать пост</h4>
    <post-input
        v-model.trim="post.title"
        type="text"
        placeholder="Название"
    ></post-input>
    <post-input
        v-model.trim="post.description"
        type="text"
        placeholder="Описание"
    ></post-input>
    <post-button
        style="align-self: flex-end; margin-top: 15px"
        @click="createPost"
    >
      Создать
    </post-button>
  </form>

</template>

<script>
export default {
  name: "PostForm",
  data() {
    return {
      post: {
        title: '',
        description: '',
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post);
      this.post = {
        title: '',
        description: '',
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
</style>
