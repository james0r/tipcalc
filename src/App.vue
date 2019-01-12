<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>TIP</span>
        <span class="font-weight-light">CALCULATOR</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
      @click="openSource()"
      color="white"
      >View Source Code</v-btn>
    </v-toolbar>

    <v-content>
      <Main></Main>
    </v-content>
  </v-app>
</template>

<script>
import Main from './components/Main'

export default {
  name: 'App',
  components: {
    Main
  },
  data () {
    return {
      //
    }
  },
  methods: {
    openSource() {
      window.open('https://github.com/james0r/tipcalc/');
    }
  }
}
</script>

<style lang="scss" scoped>

</style>

