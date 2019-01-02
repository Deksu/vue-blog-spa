<template lang="html">
  <div class="post" v-if="post">
    <h1 class="post__title">{{ post.title }}</h1>
    <p class="post__body">{{ post.body }}</p>
    <p class="post__id">{{ post.id }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props: ['id'],
  data() {
    return {
      post: null,
      endpoint: 'https://jsonplaceholder.typicode.com/posts/',
    }
  },
  methods: {
      // getting one post per identifier
      getPost(id) {
          axios(this.endpoint + id)
          .then(response => {
              this.post = response.data;
          })
          .catch(error => {
              console.log(error)
          })
      }
  },
  created() {
      // calling the getPost methods outcome
      this.getPost(this.id);
  },
  watch: {
    // Watch for the route change when the route changes when toggling posts
  '$route'() {
    this.getPost(this.id);
  }
}
}
</script>
