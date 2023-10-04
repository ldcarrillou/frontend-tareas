<template>
  <!--img alt="Vue logo" src="./assets/logo.png"-->
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <Tarea/>
</template>

<script>
//import HelloWorld from './components/HelloWorld.old.vue'
import Tarea from './components/Tarea.vue'

export default {
  name: 'App',
  components: {
    //HelloWorld
    Tarea
  }
}
</script>

<style>
/*#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}*/
</style>
