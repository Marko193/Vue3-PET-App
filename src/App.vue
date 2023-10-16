<template>
  <div class="app">
    <h1> Страница с постами </h1>
    <div class="header-block">
      <my-button @click="showDialog">
        Create a post
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
    <div v-if="isPostsLoading">Loading...</div>
    <post-list
        v-else
        :posts="posts"
        @remove="deletePost"
    />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import MyDialog from "@/components/UI/MyDialog.vue";
import MyButton from "@/components/UI/MyButton.vue";
import axios from "axios";
import MySelect from "@/components/UI/MySelect.vue";

export default {
  components: {
    MySelect,
    MyButton,
    MyDialog,
    PostForm,
    PostList
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: false,
      selectedSort: '',
      sortOptions: [
        {value: 'title', name: 'By title'},
        {value: 'body', name: 'By body'},
      ]
    }
  },
  methods: {
    showDialog() {
      this.dialogVisible = true;
    },
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    deletePost(postId) {
      this.posts = this.posts.filter(el => el.id !== postId)
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
        this.posts = response.data;
      } catch (err) {
        alert('Error!')
      } finally {
        this.isPostsLoading = false
      }
    }
  },
  mounted() {
    this.fetchPosts()
  },
  watch: {
    selectedSort(newValue) {
      this.posts.sort((firstPost, secondPost) => {
        return firstPost[this.selectedSort]?.localeCompare(secondPost[this.selectedSort])
      })
      // console.log('newValue', newValue);
    },
  },
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

.header-block {
  display: flex;
  justify-content: space-between;
  margin: 15px 0 15px;
}

</style>
