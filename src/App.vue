<template>
  <div id="app">
    <input placeholder="filter criteria" />
    <button>Set filter criteria</button>
    <my-content v-bind:data="images"></my-content>
    <button>Load more images</button>
    <!-- feature: hamburger menu -->
  </div>
</template>

<script>
import { config } from '../config/config.js';
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
    };
  },
  created() {
    const client = this.initClient();
    client.blogPosts(`${config.name}.tumblr.com`, ((err, data) => {
      data.posts.forEach(post => {
        switch (post.type) {
          case 'photo':
            this.images.push(post);
            break;
          case 'video':
            this.videos.push(post);
            break;
          default:
            break;
        }
      });
    }).bind(this));
  },
  methods: {
    initClient: function() {
      return tumblr.createClient({
        consumer_key: config.consumer_key,
        consumer_secret: config.consumer_secret,
        token: config.token,
        token_secret: config.token_secret,
      });
    },
  },
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
