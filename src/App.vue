<template>
  <div id="app">
    <router-view></router-view>
    <my-tabbar></my-tabbar>
  </div>
</template>

<script>

  import MyTabbar from 'components/common/tabbar/MyTabbar'

  export default {
    name: 'App',
    data(){
      return {
      }
    },
    components:{
      MyTabbar
    }
  }
</script>

<style>
  @import "~assets/css/base.css";
</style>
