<template>
   <div id="file-zone">
    <div class="textArea"
        id="file"
        contenteditable="true"
        :v-bind="textArea">{{ textArea }}
    </div>
    </div>
</template>

<script>
export default {
  name: "FileZone",
  data() {
      return {
          textArea: ''
      }
  },
  methods: {
      edit(editType, showDefault, value) {
          document.execCommand(editType, showDefault, value)
      },
  },
  mounted() {
    this.$root.$on('editing', data => {        
        this.edit(data.command, data.showDef, data.value)
    })
  }

};
</script>
<style scoped>
    #file-zone {
        background-color:#f1f0f0;
        flex-grow: 1;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 5px;
    }

    #file {
        width: 600px;
        flex-grow: 1;
        background-color: #fff;
        border: 1px solid #e4dede;
    }
    .textArea {
        border: none;
        width: 100%;
        height: 100%;
        min-height: 700px;
    }
    .textArea:active {
            border: none
        }
</style>
