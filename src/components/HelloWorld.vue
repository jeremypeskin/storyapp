<template>

    <v-slide-y-transition mode="out-in">
      <v-layout>
        <div class="page page1">
          <div class="verse">
            <div :class="font" style="white-space:pre-line">
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
    },
    data: function() {
      return {}
    },
    methods: {},
    computed: {
      compiledMarkdown: function () {
        return marked(this.inputx, { sanitize: true })
      }
    },
  };
</script>