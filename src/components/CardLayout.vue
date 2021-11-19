<template>
  <div id="CardLayout">

    <h2>Titolo del film: {{ title }}</h2>
    <h2>Titolo originale: {{ original_title }}</h2>
    <div class="language">
      <h3>Lingua originale: {{ original_language }}</h3>
      <img :src="require('../assets/img/flags/flag_' + original_language + '.png')" :alt="'Language ' + original_language + ' flag'">
    </div>
    <h3>Valtazione media: {{ vote_average }}</h3>
  </div>
</template>

<script>
export default {
  name: 'CardLayout',
  props: {
    original_title: String,
    title: String,
    original_language: String,
    vote_average: Number
  }
}
</script>

<style lang="scss">
.language {
  width: 5%;
  img {
    width: 100%;
  }
}
</style>
