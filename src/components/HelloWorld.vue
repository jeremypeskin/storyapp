<template>

    <v-slide-y-transition mode="out-in">
      <v-layout app-container>
        <div class="nav-drawer-button">
          <v-btn icon @click.stop="toggleDrawer">
            <v-icon>more_vert</v-icon>
          </v-btn>
          <v-btn icon @click="print">
            <v-icon>print</v-icon>
          </v-btn>
        </div>
        <div class="page page1" :class="theme">
          <v-layout page-content row wrap>
            <v-flex class="verse" sm12 md6 >
              <v-text-field
                textarea
                :value="inputx"
                v-model="inputCopy"
                class="verse-textarea"
                v-if="editingCopy"
                @blur="doneEdit(inputCopy)"
                >
              </v-text-field>
              <div :class="font" style="white-space:pre-line" v-if="!editingCopy" @dblclick="editVerse">
                {{inputx}}
                <img :src="require('@/assets/images/' + theme + '-footer.svg')" class="footer-img"/>
              </div>
            </v-flex>
            <v-flex sm12 md6 class="images">
              <ImageSettings
                :illustrationy="illustrationxCopy"
                @illustrationWasEdited="illustrationxCopy=$event">
              </ImageSettings>
            </v-flex>
          </v-layout>
           <transition name="fade">
             <div class="page-buttons" v-if="showOptions">
               <v-btn icon v-if="index == pagesx.length-1" color="#FAF3DD" v-on:click="addNewPage">
                 <v-icon>add</v-icon>
               </v-btn>
               <v-btn icon v-if="index >= 1" color="#FAF3DD" v-on:click="removePage(pagex)">
                 <v-icon>remove</v-icon>
               </v-btn>
             </div>
           </transition>
        </div>
      </v-layout>
    </v-slide-y-transition>

</template>

<script>

  import ImageSettings from './ImageSettings'
  export default {
    props: {
      index: Number,
      font: String,
      inputx: String,
      illustrationx: String,
      editingx: Boolean,
      pagex: Object,
      pagesx: Array,
      nextPageIdx: Number,
      showOptions: Boolean,
      drawer: Boolean,
      theme: String
    },
    data: function() {
      return {
        inputCopy: this.inputx,
        illustrationxCopy: this.illustrationx,
        editedVerse: null,
        nextPageIdCopy: this.nextPageIdx,
        editingCopy: this.editingx,
        drawerCopy: this.drawer
      }
    },
    methods: {
      editVerse: function() {
        this.editingCopy = true
      },
      doneEdit: function(y) {
        this.editingCopy = false
        this.$emit('inputWasEdited', y)
      },
      addNewPage: function(){
        var that = this
        this.pagesx.push({
          input: 'Double click to edit, never forget it.',
          illustration: 'forest.png',
          editing: false,
          id: this.nextPageIdCopy++,
        })
        this.$emit('pageWasAdded', this.pagesx)
        this.$emit('pageIdUpdated', this.nextPageIdCopy)
      },
      removePage: function(page){
        var pageIndex = this.pagesx.indexOf(page);
        this.pagesx.splice(pageIndex, 1)
        this.$emit('pageWasRemoved', this.pagesx)
      },
      toggleDrawer: function(){
        console.log(this.drawer)
        this.drawerCopy = !this.drawerCopy
        console.log(this.drawer)
        this.$emit('toggleDrawer', this.drawerCopy)
      },
      print: function(){
        window.print()
      }
    },
    components: {
      ImageSettings
    },
  };
</script>