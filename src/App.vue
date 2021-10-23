<template>
  <div id="app">
    <!-- <div v-show="false">
      <h2 >Файловая система </h2>
      <fsItem
        :subSystem="initialDir"
      />
    </div> -->
    <div>
      <h2 >Файловая система </h2>
      <basket 
        v-on:clear-basket="basket.splice(0,basket.length)"
        :basket="basket"
      />
      <fs-directory
        :directoryContent="initialDir"
        :visible="true"
        v-on:select-file="selectHandler"
      />

    </div>

  </div>

</template>

<script>

import fileSystem from '../public/static/node_modules.json'
// import fsItem from './components/fsItem.vue'
import fsDirectory from "./components/fsDirectory.vue";
import Basket from './components/Basket.vue'


// const firtsDirs = fileSystem.contents.slice(0,3)
let fSys = fileSystem
// fSys.contents=firtsDirs


export default {
  name: 'App',
  components: {
    // fsItem, 
    fsDirectory,
    Basket
  },
  data () {
    return {
      initialDir: fSys,
      basket: []
    }
  },
  methods: {
    selectHandler: function(path) {
      this.basket.push(path);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
