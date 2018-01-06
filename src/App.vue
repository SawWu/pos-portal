<template>
  <div id="app">
    <Nav/>
    <router-view/>
  </div>
</template>
<style lang="less">
    @import "./assets/less/app.less";
</style>
<script>
  import Nav from '@/components/common/Nav';
  export default {
    name: 'app',
    components:{
      Nav
    }
  }
</script>

