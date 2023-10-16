<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <my-input
        type="text"
        placeholder="Название"
        v-model.trim="post.title"
    />

    <my-input
        type="text"
        placeholder="Описание"
        v-model.trim="post.body"
    />

    <my-button class="btn" @click="createPost">Create</my-button>
  </form>
</template>

<script>

export default {
  data() {
    return {
      post: {
        title: '',
        body: '',
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      // console.log('this.post', this.post)
      this.$emit('create', this.post);
      this.post = {
        title: '',
        body: '',
      }
    }
  },
  watch: {
    post: {
      handler(newVal) {
        console.log(newVal);
      },
      deep: true
    }
  },
}
</script>

<style lang="scss" scoped>

form {
  display: flex;
  flex-direction: column;
}

.btn {
  align-self: flex-end;
  margin-top: 15px;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
}

.btn:hover {
  cursor: pointer;
}
</style>
