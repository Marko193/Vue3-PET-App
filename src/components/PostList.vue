<template>
  <div v-if="posts.length > 0">
    <h3>Users list</h3>
    <Post
        v-for="post in posts"
        :post="post"
        :key="post.id"
        @remove="$emit('remove', post.id)"
    />
  </div>
  <h2 v-else class="no-posts-block">No posts available!</h2>
</template>

<script>
import Post from "@/components/Post.vue";

export default {
  components: {
    Post
  },
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.no-posts-block {
  color: red;
  text-align: center;
}
</style>
