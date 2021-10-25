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

// Нужны для отладки - сокращают кол-во папок
// const firtsDirs = fileSystem.contents.slice(0,3)
let fSys = fileSystem
// fSys.contents=firtsDirs


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
      selectedFileComponent: {}
    }
  },
  methods: {
    selectHandler: function(path, newSelectedFileComponent) {
      if (this.selectedFile != '') {
        console.log("old file: " + this.selectedFileComponent.fileContent.name)
        this.selectedFileComponent.unselect();
      }
      this.selectedFileComponent=newSelectedFileComponent;
      console.log("new file: " + this.selectedFileComponent.fileContent.name)
      this.selectedFile =path;
    },
    unselectHandler: function() {
      this.selectedFileComponent.unselect();
      this.selectedFileComponent = {}
      this.selectedFile=''
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
