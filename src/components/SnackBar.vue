<template>
  <div>
    <v-snackbar
      style="z-index:1;"
      :timeout="timeout"
      :color="color"
      :multi-line="mode === 'multi-line'"
      :vertical="mode === 'vertical'"
      v-model="snackbars[n].show"
      :top="snackbars[n].y === 'top'"
      :bottom="snackbars[n].y === 'bottom'"
      :right="snackbars[n].x === 'right'"
      :left="snackbars[n].x === 'left'"
      >
      {{ snackbars[n].text }}
      <v-btn dark flat @click.native="n++">GOT IT!</v-btn>
    </v-snackbar>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        n:0,
        snackbars: [
          {
            show: true,
            text: "Click that image 👆 to change it.",
            x:'right',
            y:'bottom',
          },
          {
            show: true,
            text: "Double click that text below 👇 to edit it.",
            x:'left',
            y:'top',
          },
          {
            show: true,
            text: "👈 Click that plus sign to create a new page.",
            x:'middle',
            y:'bottom',
          },
          {
            show: true,
            text: "👈 Click those three dots to style your page.",
            x:'middle',
            y:'top',
          },
          {
            show: true,
            text: "👈 When you're done, click that print button to save your story.",
            x:'middle',
            y:'top',
          },
          {}
        ],
        color: 'info',
        timeout: null,
        mode: '',
      }
    }
  }
</script>

<style>
</style>