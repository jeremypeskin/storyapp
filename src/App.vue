<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app>
      <PageSettings :font="fontFamily" @fontWasEdited="fontFamily = $event"></PageSettings>
      <v-btn v-on:click="addPage">New Page</v-btn>
    </v-navigation-drawer>
    <v-toolbar app>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
    </v-toolbar>
    <v-content>
      <HelloWorld
        v-for="page in pages"
        :font="fontFamily"
        :inputx="page.input"
        :illustrationx="page.illustration"
        :editingx="page.editing"
        @inputWasEdited="page.input = $event">
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
          input:
            'Double click to edit, never forget it.',
          illustration: 'forest.png',
          editing: false
        }
      ],
      drawer: false,
      fontFamily: 'blackAndWhite',
    }
  },
  name: 'App',
  components: {
    HelloWorld,
    PageSettings,
    ImageSettings
  },
  methods: {
    addPage: function(){
      this.pages.push({
        input:
          'Double click to edit, never forget it.',
        illustration: 'forest.png',
        editing: false
      })
    }
  }
}
</script>
