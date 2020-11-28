<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png">-->
    <construction-page msg="Welcome to m4Dragon.io!"/>
    <construction-footer id="footer"/>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import ConstructionPage from "./components/ConstructionPage";
import ConstructionFooter from "./components/ConstructionFooter";

export default {
  name: 'App',
  components: {
    //HelloWorld
    ConstructionPage,
    ConstructionFooter,
  }
}
</script>

<style>
body {
  background-image: url("assets/parchment-as-background.jpg");
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: grid;
  grid-template-areas:
    "header"
    "body"
    "footer";
}
#footer {
  grid-area: footer;
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 2.5rem;
  justify-content: space-between;
}
</style>