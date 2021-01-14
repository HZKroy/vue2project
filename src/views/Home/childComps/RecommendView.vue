<template>
  <div class="recommend-view">
    <div v-for="item in recommends" :key="item.value" class="recommend-view-item">
      <a :href="item.link">
        <img :src="item.image" alt="">
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RecommendView',
  props: {
    recommends: {
      type: Array,
      default(){
        return []
      }
    }
  },
  components:{
  }
}
</script>

<style scoped>
  .recommend-view{
    display: flex;
    width: 100%;
    text-align: center;
    padding: 15px 0 30px 0;
    border-bottom: 10px solid #eee;
  }
  .recommend-view-item{
    flex: 1;
  }
  .recommend-view-item img{
    width: 80px;
    height: 80px;
  }
</style>
