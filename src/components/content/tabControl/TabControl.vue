<template>
  <div class="tab-control">
    <div v-for="(item,index) in titles" :key="item.value" class="tab-control-item" :class="{active:index==currentIndex}" @click="tabItemClick(index)">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'TabControl',
    data(){
      return {
        currentIndex:0
      }
    },
    props: {
      titles:{
        type:Array,
        default(){
          return []
        }
      }
    },
    components:{
    },
    methods:{
      tabItemClick(index){
        this.currentIndex=index
        this.$emit('tabClick',index)
      }
    }
  }
</script>

<style scoped>
  .tab-control{
    display: flex;
    text-align: center;
    font-size: 15px;
    background-color: #fff;
  }
  .tab-control-item{
    flex: 1;
    height: 40px;
    line-height: 40px;
  }
  .active{
    color: rgb(214, 42, 65);
  }
  .active span{
    border-bottom: 3px solid rgb(214, 42, 65);
    padding: 5px;
  }
</style>
