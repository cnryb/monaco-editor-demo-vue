<template>
  <div id="app">
    <DiffEditor class="editor"  :originalValue="diff.original" :modifiedValue="diff.modifield" />
  </div>
</template>

<script>
import DiffEditor from "./components/DiffEditor.vue";

export default {
  name: 'App',
  components: {
    DiffEditor
  },
  data(){
    return {
      diff:{
        original:`好言难得，恶语易施
一言既出，驷马难追
.


常将有日思无日，莫把无时当有时。

ho


ha

!`,
        modifield:`好言难得，恶语易施
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
</style>
