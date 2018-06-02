<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app>
      <PageSettings :font="fontFamily" @fontWasEdited="fontFamily = $event"></PageSettings>
    </v-navigation-drawer>
    <v-toolbar app v-show="showOptions">
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
    </v-toolbar>
    <v-content>
      <HelloWorld
        v-for="(page, index) in pages"
        :index="index"
        :font="fontFamily"
        :pagex="page"
        :pagesx="pages"
        :nextPageIdx="nextPageId"
        :inputx="page.input"
        :illustrationx="page.illustration"
        :editingx="page.editing"
        :key="page.id"
        :showOptions="showOptions"
        @inputWasEdited="page.input = $event"
        @pageWasAdded="pages=$event"
        @pageIdUpdated="nextPageId=$event"
        @pageWasRemoved="pages=$event"
        >
      </HelloWorld>
    </v-content>
  </v-app>
</template>

<script>

import HelloWorld from './components/HelloWorld'
import PageSettings from './components/PageSettings'
import ImageSettings from './components/ImageSettings'

export default {
  data () {
    return {
      pages: [
        {
          input:'Double click to edit, never forget it.',
          illustration: 'forest.png',
          editing: false,
          id:1
        }
      ],
      drawer: false,
      fontFamily: 'blackAndWhite',
      nextPageId:2,
      showOptions:false
    }
  },
  name: 'App',
  components: {
    HelloWorld,
    PageSettings,
    ImageSettings
  },
  methods: {
    displayOptions(){
      console.log("Mouse moved!")
    }
  },
  mounted: function(){
    var that = this
    window.onmousemove = function(){
      that.showOptions=true
      if (page.editing===false) {
        setTimeout(function(){
          that.showOptions=false
        }, 3000);
      }
    }.bind(this)
  }
}
</script>
