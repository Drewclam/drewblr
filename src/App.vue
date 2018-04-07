<template>
  <div id="app">
    <input placeholder="filter criteria" />
    <button>Set filter criteria</button>
    <button v-on:click="renderPosts(limit += 20)">Load Posts</button>
    <my-content v-bind:posts="posts"></my-content>
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
      limit: 20,
    };
  },
  computed: {
    client: function() {
      return this.initClient();
    },
  },
  created() {
    this.renderPosts(this.limit);
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
    getPosts: function(client, limit) {
      return client
        .blogPosts(`${config.name}.tumblr.com`, {limit: limit, offset: limit})
        .then((res) => res.posts)
        .catch((err) => console.error(err));
    },
    renderPosts: function(limit) {
      console.log(limit);
      this.getPosts(this.client, limit).then((posts) => {
        console.log('retrieved posts: ', posts);
        this.posts = posts;
      });
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
