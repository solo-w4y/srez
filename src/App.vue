<template>
  <div id="app">
    <ShirtForm />
  </div>
</template>

<script>
import ShirtForm from './components/ShirtForm.vue'

export default {
  name: 'App',
  components: {
    ShirtForm
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
