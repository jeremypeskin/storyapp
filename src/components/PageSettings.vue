<template>
  <div>
    <v-select
      :items="fontOptions"
      v-model="fontCopy"
      label="Select"
      single-line
      v-on:input="newFont(fontCopy)"
      hint= "Choose a font"
      persistent-hint
      >
    </v-select>
    <v-select
      :items="themeOptions"
      v-model="themeCopy"
      label="Select"
      single-line
      v-on:input="newTheme(themeCopy)"
      hint= "Choose a theme"
      persistent-hint
      >
    </v-select>
  </div>
</template>

<script>
  export default {
    props: ['font', 'theme', 'inputx'],
    data: function() {
      return {
        themeCopy: this.theme,
        themeOptions: [
          { text: 'Nature', value: 'nature' },
          { text: 'Space', value: 'space' },
          { text: 'Winter', value: 'winter' }
        ],
        fontCopy: this.font,
        fontOptions: [
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
      newTheme: function(x) {
        this.$emit('themeWasEdited', x)
      }
    },
  };
</script>