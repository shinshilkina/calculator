<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Бульбулятор</h1>
    <Calculator />
  </div>
</template>

<script>
import Calculator from "./components/Calculator";

export default {
  name: 'app',
  components: {Calculator},
  data () {
    /*...*/
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200&display=swap');
#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  font-weight: normal;
}
img {
  width: 5vh;
  height: 5vh;
}
</style>
