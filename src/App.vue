<template>
  <div id="app">
    <input placeholder="filter criteria" />
    <button>Set filter criteria</button>
    <my-content v-bind:posts="posts"></my-content>
    <button v-on:click="getPosts">Load more images</button>
    <!-- feature: hamburger menu -->
  </div>
</template>

<script>
import config from '../config/config.js';
import tumblr from 'tumblr.js';

import MyContent from './components/my-content';

export default {
  name: 'App',
  components: {
    MyContent,
  },
  data() {
    return {
      images: [],
      videos: [],
      posts: null,
    };
  },
  created() {
    const client = this.initClient();

    this.getPosts(client).then((posts) => this.posts = posts);
  },
  methods: {
    initClient: function() {
      return tumblr.createClient({
        credentials: {
          consumer_key: config.consumer_key,
          consumer_secret: config.consumer_secret,
          token: config.token,
          token_secret: config.token_secret,
        },
        returnPromises: true,
      });
    },
    getPosts: function(client) {
      return client
        .blogPosts(`${config.name}.tumblr.com`)
        .then((res) => res.posts)
        .catch((err) => console.error(err));
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
