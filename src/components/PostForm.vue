<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <custom-input
        v-model:value="post.title"
        type="text"
        placeholder="Название поста"/>

    <custom-input
        v-model:value="post.body"
        type="text"
        placeholder="Описание поста"/>

    <my-button @click="createPost"
               style="align-self: flex-end; margin-top: 15px"
            class="createPost">Создать пост</my-button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost(){
      this.post.id = Date.now();
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: ''
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