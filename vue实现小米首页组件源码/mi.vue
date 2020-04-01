<template>
  <div>
    <nav-header></nav-header>
    <router-view></router-view>
  </div>
</template>

<script>
import NavHeader from "./NavHeader";
export default {
  // name:'nav-home'
  components: {
    NavHeader
  }
};
</script>

<style lang="scss" scoped>
</style>