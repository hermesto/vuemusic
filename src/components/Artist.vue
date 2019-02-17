<template lang="pug">
  li.artist
    h2: a(:href="artist.url" target="_blank") {{artist.name}}
    img(:src="artist.image[2]['#text']")
</template>

<script>
export default {
    name: 'artist',
    props: ['artist']
}
</script>

<style lang="stylus" scoped>
li.artist
  margin 20px 20px
  background-color rgba(255,255,255,0.8)
</style>
