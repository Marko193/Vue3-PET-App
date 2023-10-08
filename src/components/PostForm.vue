<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <input
        type="text"
        class="input"
        placeholder="Название"
        v-model="post.title"
    >

    <input
        type="text"
        class="input"
        placeholder="Описание"
        v-model="post.body"
    >

    <button class="btn" @click="createPost">Create</button>
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
      this.$emit('create', this.post);
      this.post = {
        title: '',
        body: '',
      }
    }
  }
}
</script>

<style lang="scss" scoped>

form {
  display: flex;
  flex-direction: column;
}

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 10px;
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