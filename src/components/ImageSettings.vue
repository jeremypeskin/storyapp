<template>
  <v-layout>
    <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
      <v-btn color="primary" dark slot="activator">Select Image</v-btn>
      <v-card>
        <v-toolbar dark color="primary">
          <v-btn icon @click.native="dialog = false" dark>
            <v-icon>close</v-icon>
          </v-btn>
          <v-toolbar-title>Select an Image</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-toolbar-items>
            <v-btn dark flat @click.native="dialog = false">Save</v-btn>
          </v-toolbar-items>
        </v-toolbar>
        <v-container fluid grid-list-xl>
           <v-layout row wrap>
             <v-flex xs4 justify-height v-for="image in images">
              <img :src="require('@/assets/images/' + image.url)" class="listed-illustrations" @click="newImage(image)"/>
            </v-flex>
          </v-layout>
        </v-container>
      </v-card>
    </v-dialog>
  </v-layout>
</template>

<script>
  export default {
    props: ['illustrationx'],
    data: function() {
      return {
        dialog: false,
        images: [
          {title: 'Nature', url:'forest.png'},
          {title: 'Bees', url:'bees.png'},
          {title: 'Lion', url:'lion.png'},
          {title: 'Owls', url:'owls.png'},
          {title: 'Town', url:'town.png'},
        ]
      }
    },
    methods: {
      newImage: function(image){
        this.$emit('illustrationWasEdited', image.url)
        this.dialog = false
      }
    }
  }
</script>