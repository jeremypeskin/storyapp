<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app>
      <PageSettings :font="fontFamily" @fontWasEdited="fontFamily = $event" :inputx="input" @inputWasEdited="input = $event"></PageSettings>
      <ImageSettings :illustrationx="illustration" @illustrationWasEdited="illustration=$event"></ImageSettings>
    </v-navigation-drawer>
    <v-toolbar app>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
    </v-toolbar>
    <v-content>
      <HelloWorld :font="fontFamily" :inputx="input" :illustrationx="illustration"></HelloWorld>
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
      drawer: false,
      fontFamily: 'blackAndWhite',
      input: 'Write your verse, No need to rehearse.',
      illustration: 'forest.png'
    }
  },
  name: 'App',
  components: {
    HelloWorld,
    PageSettings,
    ImageSettings
  }
}
</script>
