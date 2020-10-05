<template>
  <div id="app">
    <main-page></main-page>
  </div>
</template>

<script>
import mainPage from '@/view/main-page.vue'

export default {
  name: 'App',
  components: {
    mainPage,
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;700&display=swap');

#app {
  font-family: 'Montserrat';
}
</style>
