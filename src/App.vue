<script>
import LnbNav from './components/LnbNav';
import { state } from './app';

function getVariableCss(name, c) {
  const rgba = (d, a) => `rgba(${d.r}, ${d.g}, ${d.b}, ${a})`;
  const rgb = d => `rgb(${d.r}, ${d.g}, ${d.b})`;
  let res = `--${name}: ${rgb(c)};`;
  for (let i = 1; i <= 9; i += 1) {
    res += `--${name}-${i}: ${rgba(c, i / 10)};`;
  }
  return res;
}

export default {
  name: 'app',
  components: {
    LnbNav,
  },
  computed: {
    isTall() {
      return this.$route.name === 'tracks' || this.$route.name === 'users' || this.$route.name === 'config';
    },
  },

  created() {
    const styleEl = document.createElement('style');
    styleEl.id = 'theme-style-tag';
    document.body.appendChild(styleEl);
    state.theme.subscribe((theme) => {
      try {
        styleEl.textContent = `body {
          ${getVariableCss('primary', theme.primary.rgba)}
          ${getVariableCss('secondary', theme.secondary.rgba)}
          ${getVariableCss('accent', theme.accent.rgba)}
        }`;
      } catch (err) { // theme is not a valid theme object
        styleEl.textContent = '';
      }
    });
  },

  mounted() {
    setTimeout(() => document.body.classList.add('transitions-active'), 200);
  },
};
</script>

<style src="./assets/scss/global.scss" lang="scss"></style>

<template>
  <main class="app" :class="{ 'app_tall': isTall }">
    <lnb-nav></lnb-nav>
    <transition enter-active-class="animated fadeInDown" leave-active-class="animated fadeOutDown">
      <router-view></router-view>
    </transition>
  </main>
</template>
