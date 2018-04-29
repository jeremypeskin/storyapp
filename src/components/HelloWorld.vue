<template>

    <v-slide-y-transition mode="out-in">
      <v-layout>
        <div class="page page1">
          <div class="verse">
            <v-text-field
              textarea
              :value="inputx"
              v-model="inputCopy"
              v-on:input="newInput(inputCopy)"
              class="verse-textarea"
              v-if="editingx"
              @blur="doneEdit(inputCopy)"
              >
            </v-text-field>
            <div :class="font" style="white-space:pre-line" v-if="!editingx" @dblclick="editVerse">
              {{inputx}}
            </div>
          </div>
          <div class="images">
            <img :src="require('@/assets/images/' + illustrationx)" class='z-depth-5 page-illustration'/>
          </div>
        </div>
      </v-layout>
    </v-slide-y-transition>

</template>

<script>
  export default {
    props: {
      font: String,
      inputx: String,
      illustrationx: String,
      editingx: Boolean
    },
    data: function() {
      return {
        inputCopy: this.inputx,
      }
    },
    methods: {
      newInput: function(y) {
        console.log(y)

      },
      editVerse: function() {
        this.editingx = true
      },
      doneEdit: function(y) {
        this.editingx = false
        this.$emit('inputWasEdited', y)
      }
    },
    computed: {
      compiledMarkdown: function () {
        return marked(this.inputx, { sanitize: true })
      }
    },
  };
</script>