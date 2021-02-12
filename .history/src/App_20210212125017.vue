<template>
  <HelloWorld />
  <HelloWorldVue2 />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import HelloWorldVue2 from './components/HelloWorldVue2.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    HelloWorldVue2
  }
}
</script>

<style>

</style>
