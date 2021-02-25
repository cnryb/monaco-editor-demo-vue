<template>
  <div ref="container" class="zpfe-language"></div>
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
      const languageName = 'zpfe'
      if(!monaco.languages.getLanguages().find(l=>l.id===languageName)){
        monaco.languages.register({
          id:languageName
        })
        monaco.editor.defineTheme('zpfeTheme',{
          base:'vs',
          inherit:true,
          rules:[
            // {
            //   token:'keyword',
            //   foreground:'ff00ff'
            // },
            {
              token:'error',
              foreground:'ff0000',
              fontStyle:'bold'
            }
          ]
        })

        const keywords = ['and','or']
        const root = [
                      [/!\[.+?\]/, 'error'],
                      [/[a-z_$][\w$]*/, {
                        cases: {
                          '@keywords': 'keyword'
                        }
                      }]
                    ]
        monaco.languages.setMonarchTokensProvider(languageName,{
          keywords,
          tokenizer:{
            root
          }
        })


      }

      this.monacoEditor = monaco.editor.create(this.$refs.container,{
        value: `![error123123] and abc or 123`,
        language: 'zpfe',
        theme: 'zpfeTheme',
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
.zpfe-language{
  height: 200px;
}
</style>
