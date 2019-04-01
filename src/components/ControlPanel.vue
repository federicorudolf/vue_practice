<template>
   <div id="control-panel">
        <div id="format-actions">
            <button
                v-for="(button) in buttons"
                :key=button.command
                className="format-action"
                v-on:click="edit(button.command, button.showDef, button.value)"
                type="button"><b>{{ button.name }}</b></button>
            <input type="text" v-model="getSynonim" class="alignRight">
            <button v-on:click="getSynonims" class="alignRight">Get synonims</button>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "ControlPanel",
  data() {
      return {
          buttons: {
              bold: {
                  command: 'bold',
                  showDef: false,
                  value: '',
                  name: 'Bold'
              },
              italic: {
                  command: 'italic',
                  showDef: false,
                  value: '',
                  name: 'Italic'
              },
              underline: {
                  command: 'underline',
                  showDef: false,
                  value: '',
                  name: 'Underline'
              },
              justifyCenter: {
                  command: 'justifyCenter',
                  showDef: false,
                  value: '',
                  name: 'Center'
              },
              justifyRight: {
                  command: 'justifyRight',
                  showDef: false,
                  value: '',
                  name: 'Right'
              },
              justifyLeft: {
                  command: 'justifyLeft',
                  showDef: false,
                  value: '',
                  name: 'Left'
              }
          },
          getSynonim: '',
          synonims: ['']
      }
  },
  methods: {
      edit(command, showDef, value) {
          this.$root.$emit('editing', {command: command, showDef: showDef, value: value})
      },
      getSynonims() {
        axios.get(`https://api.datamuse.com/words?rel_syn=${this.getSynonim}`)
             .then(res => {
                 res.data.forEach(element => {
                     this.synonims.push(element.word)
                 });
                 this.$emit('gotSynonims', this.synonims)
             }, err => {
                 console.log(err);
             })
      }
  }
};
</script>
<style scoped>
    #control-panel {
        background-color: #fff;
        height: 25px;
        display: flex;
        align-items: center;
        flex-direction: column;
        padding-top: 5px;
    }
    .alignRight {
        align-self: flex-end;
    }
</style>
