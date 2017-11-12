<script>
export default {
  components: { },
  data: () => ({
    episode: 199,
    title: 'latenight.blue',
  }),
};
</script>

<template>
  <header class="lnb-header">
    <a
      href="/"
      title="latenight.blue"
      class="lnb-header__title"
    >
      <h1>{{ title }}</h1>
    </a>
    <div class="lnb-header__episode">
      episode {{ episode }}
    </div>
  </header>
</template>
