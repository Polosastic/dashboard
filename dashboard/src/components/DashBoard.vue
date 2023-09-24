<template>
  <div class="hello">
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
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #0f0a55;
}
a.active{
    color:green;
}
nav{
  padding-bottom: 20px;
  text-align: left;
}
.logo img{
  width: 30px;
  height:30px;
}
</style>
