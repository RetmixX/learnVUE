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
import PostList from "@/components/PostList.vue"

export default {
  components: {
    PostForm,
    PostList
  },

  data() {
    return {
      posts: [
        {
          id: 1,
          title: 'Пост о джаве',
          body: 'Какая-то душная фигня'
        },
        {
          id: 2,
          title: 'Спринг секурити',
          body: 'Данная статья про то, как вы  свое время'
        },
        {
          id: 3,
          title: 'Xz',
          body: 'xzxzxzxz'
        }
      ],
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
    },
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