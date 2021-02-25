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
      monaco.languages.registerCompletionItemProvider('json', {
        triggerCharacters: ['！', '!'],
        // eslint-disable-next-line
        provideCompletionItems: (model, position, context, token) => {
          const inputChar = model.getLineContent(position.lineNumber)[position.column - 2]
          console.log(inputChar)
          const suggestions = []
          suggestions.push({
                label: `![error]`,
                kind: monaco.languages.CompletionItemKind.Variable,
                detail: `description`,
                documentation: 'documentation documentation documentation documentation',
                insertText: `！【error】 `
              })

          return {
            suggestions
          }
        }
      })
      this.monacoEditor = monaco.editor.create(this.$refs.container, {
          value: `![error123123] and abc or 123  `,
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