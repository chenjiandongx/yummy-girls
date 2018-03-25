<template>
  <div id="app">
    <imgs-list></imgs-list>
  </div>
</template>

<script>
import imgsList from './components/imgs-list';
import PulseLoader from 'vue-spinner/src/PulseLoader.vue';

export default {
  name: 'App',
  components: {
    imgsList,
      PulseLoader
  }
}
</script>

<style>
  .container {
    height: 100%;
    width: 100%;
    position: absolute;
  }

</style>
