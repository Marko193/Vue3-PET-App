<template>
  <div class="app">
    <post-form
        @create="createPost"
    />
    <post-list
        :posts="posts"
        @remove="deletePost"
    />
  </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import post from "@/components/Post.vue";

export default {
  components: {
    PostForm,
    PostList
  },
  data() {
    return {
      posts: [
        {id: 1, title: 'JavaScript', body: 'Описание №1'},
        {id: 2, title: 'C++', body: 'Описание №2'},
        {id: 3, title: 'Python', body: 'Описание №3'}
      ]
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      // console.log('post', post);
    },
    deletePost(postId){
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
