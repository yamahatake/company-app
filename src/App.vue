<template>
  <div id="app">
    <headerMain/>
    <contentMain/>
    <footerMain/>
  </div>
</template>

<script>
import headerMain from './components/layout/headerMain.vue';
import contentMain from './components/layout/contentMain.vue';
import footerMain from './components/layout/footerMain.vue';

export default {
  name: 'app',
  components: {
    'headerMain': headerMain,
    'contentMain': contentMain,
    'footerMain': footerMain
  }
}
</script>

<style lang="scss">
  @import "@/assets/styles/main.scss";
</style>