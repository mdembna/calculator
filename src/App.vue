<template>
  <div id="app">
    <Calculator/>
  </div>
</template>

<script>
import Calculator from './components/Calculator'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
#app {
  min-height: 100vh;
  background-image: url(./assets/plant3.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 100px 0px;
  background-color: rgba(0, 0, 0, 0.1);
  margin: 0px;
}
</style>
