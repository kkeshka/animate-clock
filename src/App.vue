<template>
  <div id="app">
    <main class="main">
      <clock-comp :dataType="'hours'"/>
      <clock-comp :dataType="'mins'" :clockColor="'#f53d3d'"/>
      <clock-comp :clockColor="'#cb3efa'"/>
    </main>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

import ClockComp from '@/components/clock-comp.vue'

export default Vue.extend({
  components: {
    ClockComp
  }
})
</script>

<style lang="scss">
html {
  box-sizing: border-box;
  width: 100%;
  height: 100%;
    background: #575757;
}

body {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  // padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

.main {
  display: flex;
  flex-wrap: 30px;
  padding: 30px;
  width: 100%;
  height: 100%;
  justify-content: space-evenly;
  flex-wrap: wrap;
}
</style>
