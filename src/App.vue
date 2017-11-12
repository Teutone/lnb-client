<script>
import LnbHeader from './components/LnbHeader';

export default {
  name: 'app',
  components: {
    LnbHeader,
  },

  created() {
    document.title = 'latenight.blue';
  },
};
</script>

<style src="./assets/scss/global.scss" lang="scss"></style>
<style src="./assets/latenight.blue/scss/index.scss" lang="scss"></style>

<template>
  <main id="main">
    <lnb-header></lnb-header>
    <lnb-song></lnb-song>
  </main>
</template>
