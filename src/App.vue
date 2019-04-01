<template>
  <div id="app">
    <Header/>
    <main>
      <ControlPanel @gotSynonims="showSynonims"></ControlPanel>
      <FileZone/>
    </main>
    <div v-if="synonims.length" id="synonims">
      <span>Synonims: </span>
      <span v-for="(synonim, index) in synonims" :key=index> {{ synonim }} </span>
    </div>
  </div>
</template>

<script>
import ControlPanel from './components/ControlPanel'
import FileZone from './components/FileZone'
import Header from './components/Header'

export default {
  name: 'App',
  components: {
    Header,
    ControlPanel,
    FileZone
  },
  data() {
    return {
      synonims: []
    }
  },
  methods: {
    showSynonims(synonims) {
      this.synonims = synonims
      console.log(synonims);
    }
  }
}
</script>

<style>
#app {
  display: flex;
  height: 100%;
  flex-direction: column;
}
main {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}
#synonims {
  float: right;
  position: absolute;
  top: 100px;
  right: 15px;
  display: flex;
  flex-flow: column;

}
</style>
