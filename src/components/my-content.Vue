<template class="flex w-100 flex-wrap">
  <div v-if="data">
    <img 
      v-for="(image, index) in data"
      v-if="image.photos"
      v-bind:key="index"
      v-bind:src="image.photos[0].original_size.url" />
      <!-- v-bind:height="post.photos[0].alt_sizes[4].height"
      v-bind:width="post.photos[0].alt_sizes[4].width" -->
  </div>
</template>

<script>
export default {
  name: 'MyContent',
  props: ['data'],
}
</script>