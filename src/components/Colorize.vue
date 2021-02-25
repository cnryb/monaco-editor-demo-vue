<template>
  <pre ref="container" data-lang="csharp">
/* 这种着色方式，不支持折叠代码 */

using System;

namespace HelloWorld
{
  class Program
  {
    static void Main(string[] args)
    {
      Console.WriteLine("天地玄黄，日月洪荒。");
    }
  }
}

</pre>
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
      monaco.editor.colorizeElement(this.$refs.container)

    }
  }
}

</script>
