<template>
  <div class="main-layout">
    <main class="main-wrapper">
      <router-view />
    </main>
  </div>
</template>

<script>
export default {
  name: 'MainLayout'
}
</script>

<style lang="scss" scoped>
  .main-wrapper {
    height: 100%;
  }
</style>
