<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app>
      <!--<PageSettings :font="fontFamily" @fontWasEdited="fontFamily = $event" :inputx="input" @inputWasEdited="input = $event"></PageSettings>-->
      <!--<ImageSettings :illustrationx="illustration" @illustrationWasEdited="illustration=$event"></ImageSettings>-->
    </v-navigation-drawer>
    <v-toolbar app>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
    </v-toolbar>
    <v-content>
      <HelloWorld v-for="page in pages" :font="fontFamily" :inputx="page.input" :illustrationx="page.illustration"></HelloWorld>
    </v-content>
  </v-app>
</template>

<script>

import HelloWorld from './components/HelloWorld'
//import PageSettings from './components/PageSettings'
//import ImageSettings from './components/ImageSettings'

export default {
  data () {
    return {
      pages: [
        {input: 'Write your verse, No need to rehearse.',
        illustration: 'forest.png'}
      ],
      drawer: false,
      fontFamily: 'blackAndWhite',
    }
  },
  name: 'App',
  components: {
    HelloWorld,
    //PageSettings,
    //ImageSettings
  }
}
</script>
