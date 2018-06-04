<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app>
      <PageSettings
        :font="fontFamily"
        :theme="theme"
        @fontWasEdited="fontFamily = $event"
        @themeWasEdited="theme = $event"
        ></PageSettings>
    </v-navigation-drawer>
    <!--<v-toolbar app v-show="showOptions">
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
    </v-toolbar>-->
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
        :drawer="drawer"
        :theme="theme"
        @inputWasEdited="page.input = $event"
        @pageWasAdded="pages=$event"
        @pageIdUpdated="nextPageId=$event"
        @pageWasRemoved="pages=$event"
        @toggleDrawer="drawer=$event"
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
          id:1,
        }
      ],
      drawer: false,
      fontFamily: 'blackAndWhite',
      nextPageId:2,
      showOptions:false,
      theme: 'nature'
    }
  },
  name: 'App',
  components: {
    HelloWorld,
    PageSettings,
    ImageSettings
  },
  mounted: function(){
    var that = this
    window.onmousemove = function(){
      that.showOptions=true
    }.bind(this)
  }
}
</script>
