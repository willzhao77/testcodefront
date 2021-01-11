<template>
  <ShowUniversities msg="Welcome to Your Vue.js App"/>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import ShowUniversities from './components/ShowUniversities.vue'

export default {
  name: 'App',
  components: {
    ShowUniversities
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color:  #2c3e50;
  margin-top: 20px;
}

  html,body,#app{
    height:100%;
}

</style>
