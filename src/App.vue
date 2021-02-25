<template>
  <div id="app">
    <SimpleEditor v-if="showSimple" class="editor" :editorOptions="editorOptions"/>
    <DiffEditor v-if="showDiff"   :originalValue="diff.original" :modifiedValue="diff.modifield" />
    <Colorize />
    <!-- <CustomLanguageColorize /> -->
    <AutoComplete />
    <Hover />
  </div>
</template>

<script>
import DiffEditor from "./components/DiffEditor.vue";
import SimpleEditor from "./components/SimpleEditor.vue"
import Colorize from "./components/Colorize.vue"
import CustomLanguageColorize from "./components/CustomLanguageColorize.vue"
import AutoComplete from "./components/AutoComplete.vue"
import Hover from "./components/Hover.vue"

export default {
  name: 'App',
  components: {
    DiffEditor,
    SimpleEditor,
    Colorize,
    CustomLanguageColorize,
    AutoComplete,
    Hover
  },
  data(){
    return {
      showSimple:true,
      showDiff:false,

      editorOptions: {
        language: 'csharp',
        value: 'string str = "hello world";',
        contextmenu: false, // 右键菜单
        scrollBeyondLastLine: false,
        minimap: {
          enabled: false,
        },
      },
      diff:{
        modifield:`好言难得，恶语易施
一言既出，驷马难追
.


常将有日思无日，莫把无时当有时。

ho


ha

!`,
        original:`好言难得，恶语易施
君子一言，快马一鞭
!


常将有日思无日，莫把无时当有时.

ho


哈

!`
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.editor{
  height: 200px;
}
</style>
