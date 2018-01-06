<template>
  <div id="app">
    <Nav/>
    <div class="main">
      <router-view/>
    </div>
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

