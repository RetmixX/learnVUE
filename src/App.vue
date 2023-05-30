<template>
  <div class="app">
    <h2>Страница с постами</h2>
    <custom-input
        v-model:value="searchPostQuery"
        placeholder="Поиск"
    />
    <div class="button__create">
      <my-button
          @click="showDialog"
          style="margin: 10px 0"
      >Создать пост
      </my-button>
      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      >

      </my-select>
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form
          @create="createPost"
      />
    </my-dialog>
    <post-list
        :posts="sortedAndSearchPosts"
        @delete="deletePost"
        v-if="!isPostLoading"
    />
    <div v-else class="container__loader">
      <span class="loader"></span>

    </div>
  </div>
</template>

<script>

import PostList from "@/components/PostList.vue";
import PostForm from "@/components/PostForm.vue";
import axios from "axios";

export default {
  components: {PostList, PostForm},

  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostLoading: false,
      selectedSort: '',
      searchPostQuery: '',
      sortOptions: [
        {value: 'title', name: 'Название'},
        {value: 'body', name: 'Содержимое'},
      ]
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    deletePost(post) {
      this.posts = this.posts
          .filter(p => p.id !== post.id)
    },

    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts() {
      try {
        this.isPostLoading = true;
        setTimeout(async () => {
          const responsePosts = await axios
              .get('https://jsonplaceholder.typicode.com/posts?_limit=10');
          this.posts = responsePosts.data;
          this.isPostLoading = false;
        }, 1)
      } catch (e) {
        alert(e)
      }
    },

  },

  mounted() {
    this.fetchPosts();
  },

  computed: {
    sortedPost() {
      return [...this.posts].sort((postOne, postTwo) =>
          postOne[this.selectedSort]?.localeCompare(postTwo[this.selectedSort]))
    },
    sortedAndSearchPosts() {
      return this.sortedPost.filter(post=>post.title.toLowerCase().includes(this.searchPostQuery.toLowerCase()))

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


.loader {
  width: 48px;
  height: 48px;
  border: 5px solid #FFF;
  border-bottom-color: brown;
  border-radius: 50%;
  display: inline-block;
  box-sizing: border-box;
  animation: rotation 1s linear infinite;
}

.button__create {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}

.container__loader {
  display: flex;
  align-items: center;
  justify-content: center;
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>