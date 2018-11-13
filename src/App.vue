<template>
  <div id="app">
    <vueMagnifier :small-img="img" :big-img="img"></vueMagnifier>
  </div>
</template>

<script>
  import vueMagnifier from './plugin/vue-magnifier'

  export default {
    name: 'app',
    data () {
      return {
        img: 'https://img14.360buyimg.com/n0/jfs/t24805/157/2124915071/151670/46286f4c/5bc57738Naf8c2ca3.jpg'
      }
    },
    components: {
      vueMagnifier
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
    /*margin-top: 60px;*/
  }

  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>
