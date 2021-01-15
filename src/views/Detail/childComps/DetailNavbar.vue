<template>
  <div class="detail-navbar">
    <navbar>
      <div slot="left" class="back" @click="backClick"><img src="~assets/img/common/back.svg" alt=""></div>
      <div slot="center" class="title">
        <div v-for="(item,index) in titles" :key="index" class="title-item" :class="{active:index===currentIndex}" @click="titleClick(index)">{{item}}</div>
      </div>
    </navbar>
  </div>
</template>

<script>
  import Navbar from 'components/common/navbar/Navbar'
  export default {
    name: 'DetailNavbar',
    data(){
      return {
        titles:['商品','参数','评论','推荐'],
        currentIndex:0,

      }
    },
    props: {
    },
    components:{
      Navbar
    },
    methods:{
      titleClick(index){
        this.currentIndex=index
      },
      backClick(){
        this.$router.back()
      }
    }
  }
</script>

<style scoped>
  .back img{
    margin-top: 12px;
  }
  .title{
    display: flex;
    font-size: 13px;
  }
  .title-item{
    flex: 1;
  }
  .active{
    color: red;
  }
</style>
