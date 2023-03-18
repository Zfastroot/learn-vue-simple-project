<script>
import { RouterLink, RouterView } from 'vue-router'
export default {
  data() {
    return {
      msg: 'Hello world!'
    }
  }
}
</script>

<template>
  <div id="app">
    <!-- As a link -->
    <nav class="navbar navbar-light bg-light">
      <a class="navbar-brand" href="/">/r/rerpuppers</a>
    </nav>


    <RouterView />
  </div>
</template>

<style scoped>

</style>
