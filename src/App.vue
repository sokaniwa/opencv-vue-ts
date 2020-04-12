<template>
  <div id="app">
    <OpenCvTest/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import OpenCvTest from './components/OpenCvSample.vue'

@Component({
  components: {
    OpenCvTest
  }
})
export default class App extends Vue {}
</script>
