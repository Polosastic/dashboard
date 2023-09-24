<template>
  <div class="header">
    <h1>{{ msg }}</h1>
  </div>
</template>
<script>
export default {
  name: 'DashBoard',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-family: cursive;
  font-weight: 700;
}
</style>
