<template>
  <div id="tabbar">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'Tabbar',
  props: {
  },
  components:{
  }
}
</script>

<style scoped>
    #tabbar{
    display: flex;
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #f6f6f6;
    height: 49px;
  }
</style>
