<template>
  <div id="app">
    <hero-carousel :autoPlay="true"/>
    <div class="container">
      <item-list />
      <!-- <img alt="Vue logo" src="@/assets/logo.png"> -->
      <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
    ItemList: () => import('./components/ItemList'),
    HeroCarousel: () => import('./components/HeroCarousel')
  }
}
</script>

<style>
#app {
  font-family: 'Belleza', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
