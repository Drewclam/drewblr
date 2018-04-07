<template class="flex w-100 flex-wrap">
  <div v-if="posts">
    <img 
      v-for="(post, index) in posts"
      v-if="post.photos"
      v-bind:key="index"
      v-bind:src="post.photos[0].original_size.url" />
      <!-- v-bind:height="post.photos[0].alt_sizes[4].height"
      v-bind:width="post.photos[0].alt_sizes[4].width" -->
  </div>
</template>

<script>
export default {
  name: 'MyContent',
  props: ['posts'],
}
</script>