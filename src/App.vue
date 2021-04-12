<template>
  <div id="app">
    <mes amountPosts="5" url="http://api.massrelevance.com/MassRelDemo/kindle.json" interval ="5000"/>
  </div>
</template>

<script>
import mes from './components/mes'

export default {
  name: 'App',
  components: {
    mes
  }
}
</script>

<style>
</style>
