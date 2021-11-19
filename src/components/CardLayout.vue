<template>
  <div id="CardLayout">

    <h2>Titolo del film: {{ title }}</h2>
    <h2>Titolo originale: {{ original_title }}</h2>
    <h3>Lingua originale: {{ original_language }}</h3>
    <img v-bind:src="flag" alt="language flag"/>
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
    vote_average: Number,
    flag: String
  }
}
</script>

<style lang="scss">
</style>
