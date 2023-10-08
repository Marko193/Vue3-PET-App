<template>
  <div>
    <h3>Users list</h3>
    <Post v-for="post in posts" :post="post" :key="post.id"/>
  </div>
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

</style>