<template class="flex w-100 flex-wrap">
  <div>
    <template v-for="(post, index) in posts">
      <img v-bind:key="index" v-if="post.type==='photo'" v-bind:src="post.photos[0].original_size.url" />
      <video v-bind:key="index" v-else v-bind:src="post.video_url" controls></video>
    </template>
  </div>
</template>

<script>
export default {
  name: 'MyContent',
  props: ['posts'],
  watch: {
    posts: function(recent, old) {
      console.log(recent.forEach(data => console.log(data.type)));
    }
  }
}
</script>