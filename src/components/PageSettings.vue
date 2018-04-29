<template>
  <div>
    <v-select
      :items="options"
      v-model="fontCopy"
      label="Select"
      single-line
      v-on:input="newFont(fontCopy)"
      hint= "Choose a font"
      persistent-hint
      >
    </v-select>

    <v-text-field
    textarea
    :value="inputx"
    v-model="inputCopy"
    v-on:input="newInput(inputCopy)"
    persistent-hint
    >
    </v-text-field>
  </div>
</template>

<script>
  export default {
    props: ['font', 'inputx'],
    data: function() {
      return {
        fontCopy: this.font,
        inputCopy: this.inputx,
        options: [
          { text: 'Fredericka', value: 'fredericka' },
          { text: 'Annie', value: 'annie' },
          { text: 'Black', value: 'blackAndWhite' }
        ],
      }
    },
    methods: {
      newFont: function(x) {
        this.$emit('fontWasEdited', x)
      },
      newInput: function(y) {
        console.log(y)
        this.$emit('inputWasEdited', y)
      }
    },
    computed: {
      compiledMarkdown: function () {
        return marked(this.input, { sanitize: true })
      }
    },
  };
</script>