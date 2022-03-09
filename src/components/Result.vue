<template>
  <div class="result">
    <div class="title" v-text="result.title" />
    <div class="desc" v-text="result.desc" />
  </div>
</template>

<script>
export default {
  props: ['result']
}
</script>
