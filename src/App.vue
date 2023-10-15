<template>
  <div class="app">
    <h1> Страница с постами </h1>
    <my-button @click="showDialog" style="margin: 15px 0 15px ">
      Create a post
    </my-button>
    <my-dialog v-model:show="dialogVisible">
      <post-form
          @create="createPost"
      />
    </my-dialog>
    <post-list
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

export default {
  components: {
    MyButton,
    MyDialog,
    PostForm,
    PostList
  },
  data() {
    return {
      posts: [
        {id: 1, title: 'JavaScript', body: 'Описание №1'},
        {id: 2, title: 'C++', body: 'Описание №2'},
        {id: 3, title: 'Python', body: 'Описание №3'}
      ],
      dialogVisible: false
    }
  },
  methods: {
    showDialog() {
      this.dialogVisible = true;
    },
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
      // console.log('post', post);
    },
    deletePost(postId) {
      // console.log('delete post', postId);
      this.posts = this.posts.filter(el => el.id !== postId)
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
