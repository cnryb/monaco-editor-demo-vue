<template>
  <div ref="container" />
</template>

<script>
import * as monaco from 'monaco-editor'

// window.MonacoEnvironment = {
//   getWorkerUrl (workerId, label) {
//     let url = 'https://fecdn2-pre.zhaopin.cn/fuxi-pre.dev/editor.worker.js'
//     if (label === 'json') {
//       url = 'https://fecdn2-pre.zhaopin.cn/fuxi-pre.dev/json.worker.js'
//     }
//     return `data:text/javascript;charset=utf-8,${encodeURIComponent(`importScripts('${url}');`)}`
//   }
// }

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
      this.monacoEditor = monaco.editor.create(this.$refs.container, this.editorOptions)
    }
  }
}

</script>
