<template>
  <div id="app">
    <div class="nav">
      <button v-for="n in navs" :key="n.title" @click="show(n.component)">{{n.title}}</button>
    </div>
    <SimpleEditor v-if="showObj.SimpleEditor" class="editor" :editorOptions="editorOptions"/>
    <DiffEditor v-if="showObj.DiffEditor"   :originalValue="diff.original" :modifiedValue="diff.modifield" />
    <Colorize v-if="showObj.Colorize" />
    <CustomLanguageColorize v-if="showObj.CustomLanguageColorize" />
    <AutoComplete v-if="showObj.AutoComplete" />
    <Hover v-if="showObj.Hover" />
    <Mark class="editor" v-if="showObj.Marker" />
  </div>
</template>

<script>
import DiffEditor from "./components/DiffEditor.vue";
import SimpleEditor from "./components/SimpleEditor.vue"
import Colorize from "./components/Colorize.vue"
import CustomLanguageColorize from "./components/CustomLanguageColorize.vue"
import AutoComplete from "./components/AutoComplete.vue"
import Hover from "./components/Hover.vue"
import Mark from "./components/Marker.vue"

export default {
  name: 'App',
  components: {
    DiffEditor,
    SimpleEditor,
    Colorize,
    CustomLanguageColorize,
    AutoComplete,
    Hover,
    Mark
  },
  data(){
    return {
      navs:[{
        title:'简单用法',
        component:'SimpleEditor'
      },{
        title:'差异对比',
        component:'DiffEditor'
      },{
        title:'简单着色',
        component:'Colorize'
      },{
        title:'自定义语言着色',
        component:'CustomLanguageColorize'
      },{
        title:'代码提示',
        component:'AutoComplete'
      },{
        title:'悬停提示',
        component:'Hover'
      },{
        title:'语法校验',
        component:'Marker'
      }],
      showObj:{
      },
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
  },
  methods:{
    show(component){
      Object.keys(this.showObj).forEach(key=>{
        this.showObj[key]=false
      })
      this.showObj[component] = true
      this.$forceUpdate()
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
  margin-top: 10px;
}
.nav{
  margin-bottom: 15px;
}
.nav button{
  margin-right: 10px;
}
.editor{
  height: 200px;
}
</style>
