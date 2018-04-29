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
              v-todo-focus="todo == editedTodo"
              >
            </v-text-field>
            <div :class="font" style="white-space:pre-line" v-if="!editingx" @dblclick="editVerse">
              {{inputx}}
            </div>
          </div>
          <div class="images">
            <ImageSettings
              :illustrationy="illustrationxCopy"
              @illustrationWasEdited="illustrationxCopy=$event">
            </ImageSettings>
          </div>
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
      editingx: Boolean
    },
    data: function() {
      return {
        inputCopy: this.inputx,
        illustrationxCopy: this.illustrationx
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
    components: {
      ImageSettings
    },
    directives: {
    'todo-focus': function (el, binding) {
      if (binding.value) {
        el.focus()
        }
      }
    }
  };
</script>