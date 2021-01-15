<template>
  <div id="app">
    <keep-alive exclude="Detail">
      <router-view></router-view>
    </keep-alive>
    <my-tabbar v-show="isTabbarActive"></my-tabbar>
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
    computed:{
      isTabbarActive(){
        return this.$route.path.indexOf('detail')===-1
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
