<template>
  <div id="app">
    <div>
      <h2 >Файловая система </h2>
      <hr>
      <fs-selection
        :selectedFile="selectedFile"
      />
      <fs-directory
        :directoryContent="initialDir"
        :visible="true"
        v-on:select-file="selectHandler"
        v-on:unselect-file="unselectHandler"
      />

    </div>

  </div>

</template>

<script>

import fileSystem from '../public/static/node_modules.json'
import fsDirectory from "./components/fsDirectory.vue";
import fsSelection from './components/fsSelection.vue'


let fSys = fileSystem

// Для отладки иставим переменную в true - сокращаем кол-во папок
const debug = false;
if (debug) {
  const firtsDirs = fileSystem.contents.slice(0,3)
  fSys.contents=firtsDirs
}


export default {
  name: 'App',
  components: {
    fsDirectory,
    fsSelection
  },
  data () {
    return {
      initialDir: fSys,
      selectedFile: '',
      selectedFileIDWrapper: {id: 0},
    }
  },
  provide() {
    return {
      selectedFileIDWrapper: this.selectedFileIDWrapper
    }
  },
  methods: {
    selectHandler: function(path, newSelectedFileID) {
      this.selectedFileIDWrapper.id=newSelectedFileID;
      this.selectedFile =path;
    },
    unselectHandler: function() {
      this.selectedFile=''
      this.selectedFileIDWrapper.id=0;
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
  max-width: 800px;
}
</style>
