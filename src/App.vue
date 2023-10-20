<template>
  <div class="app">

    <h1> Страница с постами </h1>

    <my-input v-model="searchQuery" placeholder="Search..."/>

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
        :posts="sortedAndSearchedPosts"
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
import MyInput from "@/components/UI/MyInput.vue";

export default {
  components: {
    MyInput,
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
      ],
      searchQuery: ''
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
  computed: {
    sortedPosts() {
      return [...this.posts].sort((firstPost, secondPost) => firstPost[this.selectedSort]?.localeCompare(secondPost[this.selectedSort]))
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))git
    }
  },
}
</script>
//
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
