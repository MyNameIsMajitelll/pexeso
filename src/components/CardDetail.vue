<template>
  <div :style="{ backgroundImage: 'url(' + require('@/assets/pexeso/' + id + '.jpg') + ')' }">fff</div>
</template>

<script>
export default {
  name: 'CardDetail',
  computed: {
    id() { return this.$store.state.cardDetailImage}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  div {
    height: 100%;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
  }
</style>
