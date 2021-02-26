<template>
  <div>
    <button @click="clear"> clear </button>
    <div class="container" ref="container" />
  </div>
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
    clear(){
      const model = this.monacoEditor.getModel()
      monaco.editor.setModelMarkers(model,'zpfe',[])
      const masker = monaco.editor.getModelMarkers({ owner:'zpfe' })
      console.log(masker)
    },
    initEditor () {
      this.monacoEditor = monaco.editor.create(this.$refs.container, {
        value:`// 为善最乐
// 为恶难逃
console.log('少壮不努力，老大徒伤悲')`,
        language:'javascript',
      })
      const model = this.monacoEditor.getModel()
      monaco.editor.setModelMarkers(model,'zpfe',[
        {
          startLineNumber:3,
          endLineNumber:3,
          startColumn:9,
          endColumn:12,
          message:"这地儿没错",
          severity:monaco.MarkerSeverity.Error,
          source:'开个玩笑',
          code:"haha~~"
        }
      ])
      // 数据没加载完成时，悬停错误提示，会导致控制台报错，但不影响功能。
    }
  }
}

</script>
<style scoped>
.container{
  height: 100px;
}
</style>