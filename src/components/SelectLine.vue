<template>
  <div ref="container" style="height: 200px;" />
</template>

<script>
import * as monaco from 'monaco-editor'

export default {
  props: {
    editorOptions: {
      type: Object,
      default () {
        return { }
      }
    }
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
      const editor = monaco.editor.create(this.$refs.container, {
        value: `
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 
        // 

        // 斐波那契数列
        function fibonacci(n) {
          if (n === 0 || n === 1) {
            return n;
          }
          return fibonacci(n - 1) + fibonacci(n - 2);
        }
        console.log(fibonacci(10));
        `,
        language: 'javascript',

      })
      editor.setSelection({
        startLineNumber: 27,
        endLineNumber: 27,
        startColumn: 54,
        endColumn: 0
      })
      editor.focus()
      editor.revealLineInCenter(27)
      this.monacoEditor = editor
    }
  }
}

</script>
