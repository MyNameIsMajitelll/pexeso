<template>
  <div :style="{ backgroundImage: 'url(' + require('@/assets/pexeso/' + id + '.jpg') + ')' }"></div>
</template>

<script>
export default {
  name: 'CardDetail',
  computed: {
    id() { return this.$store.state.cardDetailImage}
  }
}
</script>

<style scoped>
  div {
    height: 100%;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
  }
</style>
