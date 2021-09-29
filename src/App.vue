<template>
  <div id="app">
    <component :is="layout">
       <router-view />
    </component>
  </div>
</template>

<script>
import EmptyLayout from './layouts/EmptyLayout.vue'
import MainLayout from './layouts/MainLayout.vue'

export default {
  name: '',
  components: { EmptyLayout, MainLayout },
  data () {
    return {
    }
  },
  computed: {
    layout () {
      return `${this.$route.meta.layout || 'empty'}-layout`
    }
  }

}
</script>

<style lang="scss" scoped>
  #app {
    height: 100%;
    
    .main-layout,
    .empty-layout {
      /* height: 100%;
      min-height: 100vh; */
    }
  }
</style>
