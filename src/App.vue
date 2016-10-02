<template>
  <div id="app">
    <components :is="comp" keep-alive>
    </components>
  </div>
</template>

<script>
import Map from './components/Map'
import TypeWriter from './components/TypeWriter'
import All from './components/All'
// import Sample from './components/Sample'

export default {
  components: {
    Map,
    TypeWriter,
    All
  },
  data () {
    return {
      comp: 'TypeWriter'
    }
  },
  events: {
    greeting () {
      this.comp = 'Map'
    },
    all () {
      this.comp = 'All'
    }
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  height: 100%;
  margin:0px;
}
</style>
