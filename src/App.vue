<template>
  <div id="app">
    <rt-editor/>
  </div>
</template>

<script>
import RtEditor from './components/RtEditor';

export default {
  name: 'App',
  components: {
    RtEditor
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
