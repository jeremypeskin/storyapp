<template>

    <v-slide-y-transition mode="out-in">
      <v-layout>
        <div class="page page1">
          <div class="verse">
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
              {{inputx}}{{this.$vnode.key}}
            </div>
          </div>
          <div class="images">
            <ImageSettings
              :illustrationy="illustrationxCopy"
              @illustrationWasEdited="illustrationxCopy=$event">
            </ImageSettings>
          </div>
          <v-btn fab dark color="indigo" v-on:click="addNewPage(pagex)">
            <v-icon dark>add</v-icon>
          </v-btn>
          <v-btn fab dark color="indigo" v-on:click="removePage(pagex)">
            <v-icon dark>remove</v-icon>
          </v-btn>
        </div>
      </v-layout>
    </v-slide-y-transition>

</template>

<script>

  import ImageSettings from './ImageSettings'
  export default {
    props: {
      font: String,
      inputx: String,
      illustrationx: String,
      editingx: Boolean,
      pagex: Object,
      pagesx: Array,
      idx: Number,
      nextPageIdx: Number,
      indexx: Number
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
      },
      addNewPage: function(page){
        this.pagesx.push({
          input: 'Double click to edit, never forget it.',
          illustration: 'forest.png',
          editing: false,
          id: this.nextPageIdCopy++
        })
        console.log("The key of the current page is: " + this.$vnode.key)
        this.$emit('pageWasAdded', this.pagesx)
        this.$emit('pageIdUpdated', this.nextPageIdCopy)
        console.log("Now the nextpageid after emit is: " + this.nextPageIdCopy)
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