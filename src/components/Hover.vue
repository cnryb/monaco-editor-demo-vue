<template>
  <div ref="container" class="ac" />
</template>

<script>
import * as monaco from 'monaco-editor'

export default {
  props: {
    
  },
  data () {
    return {
      monacoEditor: null
    }
  },
  mounted () {
    this.initEditor()
  },
  methods: {
    initEditor () {
      monaco.languages.registerHoverProvider('json', {
        provideHover (model, position) {
          const lineStr = model.getLineContent(position.lineNumber)
          // position.column
          console.log(lineStr)

          return {
            contents: [
              {
                value: `**Markdown**`
              },
              {
                value: `这里用的是 _Markdown_ 语法`
              }
            ]
          }
        }
      })
      this.monacoEditor = monaco.editor.create(this.$refs.container, {
          value: `{"hover":"test"} `,
          language: 'json',
          theme: 'vs',
          contextmenu: false, // 右键菜单
          readOnly: this.readOnly, // 只读
          minimap: {
            enabled: false
          }
      })
    }
  }
}

</script>

<style scoped>
.ac{
  height: 100px;
}
</style>