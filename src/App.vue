<template>
  <div id="app" class="app">
    <div class="app__content">
      <main-page></main-page>
    </div>
    <div class="app__footer"></div>
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

.app {
  display: grid;
  grid-template-areas: "content" "footer";
  grid-template-columns: 1fr;
  grid-template-rows: auto 60px;
  font-family: 'Montserrat';

  &__content {
    grid-area: content;
  }
  &__footer {
    grid-area: footer;
  }
}
</style>
