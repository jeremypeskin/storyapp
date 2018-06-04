<template>
  <div>
    <div>
      <img :src="require('@/assets/images/' + illustrationy)" class='z-depth-5 page-illustration' v-on:click="dialog = true"/>
    </div>
    <v-layout>
      <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
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
  </div>
</template>

<script>
  export default {
    props: [
      'illustrationy',
    ],
    data: function() {
      return {
        dialog: false,
        images: [
          {title: 'Nature', url:'forest.png'},
          {title: 'Bees', url:'bees.png'},
          {title: 'Lion', url:'lion.png'},
          {title: 'Owls', url:'owls.png'},
          {title: 'Town', url:'town.png'},
          {title: 'Food', url:'food.png'},
          {title: 'Spaceman', url:'spaceman.png'},
          {title: 'Planets', url:'planets.png'},
          {title: 'Snakes', url:'snakes.png'},
          {title: 'Home', url:'home.png'},
          {title: 'Winterforest', url:'winter-forest.png'},
          {title: 'Sea', url:'sea.png'},
          {title: 'Rocket', url:'rocket.png'}
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