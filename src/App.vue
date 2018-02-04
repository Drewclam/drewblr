<template>
  <div id="app">
    <my-content
      v-bind:apiData="data">
    </my-content>
  </div>
</template>

<script>
import axios from 'axios';
import MyContent from './components/my-content';
import { config } from '../config/config.js';

export default {
  name: 'App',
  components: {
    MyContent,
  },
  created() {
    this.fetchData().then(data => this.data = data);
  },
  data() {
    return { 
      apiUrl: `https://api.tumblr.com/v2/blog/${config.name}/posts?api_key=${config.api_key}`,
      data: [],
    };
  },
  methods: {
    fetchData: function() {
      return axios.get(this.apiUrl).then(res => res.data.response.posts);
    }
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
