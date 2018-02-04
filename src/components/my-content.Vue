<template>
  <div>
    <h1>my content component</h1>
    <span
      v-for="(data, index) in apiData"
      v-bind:key="index">
      {{ data.short_url }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'MyContent',
  props: ['apiData'],
}
</script>