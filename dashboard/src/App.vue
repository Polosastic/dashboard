<template>
  <DashBoard msg="Sticky Notes Dashboard"/>
  <AddNote/>
</template>

<script>
import DashBoard from './components/DashBoard.vue'
import AddNote from './components/AddNote.vue'

export default {
  name: 'App',
  components: {
    DashBoard,
    AddNote
  }
}
</script>

<style>
* {
  background-color: rgb(202, 236, 245);
  margin:0;
}
body{
  margin: 0 auto;
}
h1 {
  font-size: 70px;
  background-image: url("./assets/post-it.jpg");
  background-size: 250px;
  background-repeat: repeat;
  color: transparent;
  -webkit-background-clip: text;
  background-clip: text;
  text-shadow: 6px 8px 11px darkcyan;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 15px;
}
</style>
