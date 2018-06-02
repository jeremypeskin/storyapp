<template>

    <v-slide-y-transition mode="out-in">
      <v-layout>
        <div class="page page1">
          <v-layout row wrap>
            <v-flex class="verse" sm12 md6 >
              <v-text-field
                textarea
                :value="inputx"
                v-model="inputCopy"
                class="verse-textarea"
                v-if="editingx"
                @blur="doneEdit(inputCopy)"
                >
              </v-text-field>
              <div :class="font" style="white-space:pre-line" v-if="!editingx" @dblclick="editVerse">
                {{inputx}}
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
               <v-btn v-if="index == pagesx.length-1" fab light color="#FAF3DD" v-on:click="addNewPage">
                 <v-icon light>add</v-icon>
               </v-btn>
               <v-btn fab light color="#FAF3DD" v-on:click="removePage(pagex)">
                 <v-icon light>remove</v-icon>
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
      showOptions: Boolean
    },
    data: function() {
      return {
        inputCopy: this.inputx,
        illustrationxCopy: this.illustrationx,
        editedVerse: null,
        nextPageIdCopy: this.nextPageIdx,
        editingCopy: this.editingx
      }
    },
    methods: {
      editVerse: function() {
        this.editingx = true
      },
      doneEdit: function(y) {
        this.editingx = false
        this.$emit('inputWasEdited', y)
        vm.$forceUpdate()
      },
      addNewPage: function(){
        this.pagesx.push({
          input: 'Double click to edit, never forget it.',
          illustration: 'forest.png',
          editing: false,
          id: this.nextPageIdCopy++
        })
        this.$emit('pageWasAdded', this.pagesx)
        this.$emit('pageIdUpdated', this.nextPageIdCopy)
      },
      removePage: function(page){
        var pageIndex = this.pagesx.indexOf(page);
        this.pagesx.splice(pageIndex, 1)
        this.$emit('pageWasRemoved', this.pagesx)
      }
    },

    components: {
      ImageSettings
    }
  };
</script>