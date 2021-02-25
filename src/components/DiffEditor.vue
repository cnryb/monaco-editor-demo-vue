<template>
<div>
  <input type="checkbox" @change="inlineChange">inline
  <button @click="nextDiff"> next diff </button>
  <div class="diff" ref="container" />
</div>

</template>

<script>
import * as monaco from 'monaco-editor'

export default {
  props: {
    originalValue:{
      type:String
    },
  modifiedValue:{
      type:String
    },
  },
  data () {
    return {
      monacoEditor: null,
      nav:null,
      inline:false
    }
  },
  mounted () {
    this.initEditor()
  },
  methods: {
    inlineChange(){
      this.inline=!this.inline

      this.monacoEditor.updateOptions({
        renderSideBySide:!this.inline
      })
    },
    nextDiff(){
      this.monacoEditor.focus()
      this.nav.next()
    },
    getEditor () {
      return this.monacoEditor
    },
    initEditor () {
      const o = monaco.editor.createModel(this.originalValue)
      const m = monaco.editor.createModel(this.modifiedValue)
      this.monacoEditor = monaco.editor.createDiffEditor(this.$refs.container,{
        enableSplitViewResizing:false,
        scrollBeyondLastLine: false,

      })
      
      this.monacoEditor.setModel({
        original: o,
        modified: m
      })
      this.nav = monaco.editor.createDiffNavigator(this.monacoEditor,{
        followsCaret:true,
        ignoreCharChanges:true
      })
    }
  }
}

</script>

<style>
.diff{
  height: 200px;
}
</style>
