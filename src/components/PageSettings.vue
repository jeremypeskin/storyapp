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
  </div>
</template>

<script>
  export default {
    props: ['font', 'inputx'],
    data: function() {
      return {
        fontCopy: this.font,
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
    },
  };
</script>