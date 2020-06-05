<template>
  <div id="app">
    <HomePage/>
  </div>
</template>

<script>
import HomePage from './components/pages/home/HomePage.vue'

export default {
  name: 'App',
  components: {
    HomePage
  }
}
</script>

<style lang="scss">
@import './assets/css/reset.css';
</style>