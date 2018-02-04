<template>
  <div id="app">
    <my-content>
    </my-content>
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
      client: null,
    };
  },
  created() {
    this.client = this.initClient();
    this.client.blogPosts(`${config.name}.tumblr.com`, function (err, data) {
      console.log(data);
      data.posts.forEach(post => console.log(post.state));
    });
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
