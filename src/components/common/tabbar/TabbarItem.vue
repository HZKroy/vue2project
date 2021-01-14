<template>
  <div id="tabbar-item" @click="itemClick">
    <slot name="item-pic-active" v-if="isActive"></slot>
    <slot name="item-pic" v-else></slot>
    <div :class="{active:isActive}"><slot name="item-text"></slot></div>
  </div>
</template>

<script>
export default {
  name: 'TabbarItem',
  data(){
    return {
    }
  },
  props: {
    path:String 
  },
  computed:{
    isActive(){
      return this.$route.path.indexOf(this.path)!==-1
    }
  },
  components:{
  },
  methods:{
    itemClick(){
      this.$router.replace(this.path)
    }
  }
}
</script>

<style scoped>
  #tabbar-item{
    flex: 1;
    text-align: center;
    font-size: 14px;
  }
    #tabbar-item img{
    width: 25px;
    height: 25px;
    margin-bottom: 3px;
  }
  .active{
    color: red;
  }
</style>
