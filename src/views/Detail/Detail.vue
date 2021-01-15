<template>
  <div class="detail">
    <detail-navbar class="detail-navbar"></detail-navbar>
    <!-- <scroll class="detail-scroll" ref="detail-scroll"> -->
      <detail-swiper :top-images="topImages"></detail-swiper>
      <detail-base-info :goods="goods"></detail-base-info>
      <detail-shop-info :shop="shop"></detail-shop-info>
      <detail-goods-info :detail-info="detailInfo" @imgLoad="imgLoad"></detail-goods-info>
      <detail-param-info :paramInfo="paramInfo"></detail-param-info>
    <!-- </scroll> -->
  </div>
</template>

<script>
  import DetailNavbar from 'views/Detail/childComps/DetailNavbar'
  import DetailSwiper from 'views/Detail/childComps/DetailSwiper'
  import DetailBaseInfo from 'views/Detail/childComps/DetailBaseInfo'
  import DetailShopInfo from 'views/Detail/childComps/DetailShopInfo'
  import DetailGoodsInfo from 'views/Detail/childComps/DetailGoodsInfo'
  import DetailParamInfo from 'views/Detail/childComps/DetailParamInfo'

  import Scroll from 'components/common/scroll/Scroll'

  import {getDetail,Goods,Shop,GoodsParam} from 'network/detail'

  export default {
    name: 'Detail',
    data(){
      return {
        iid:'',
        topImages:[],
        goods:{},
        shop:{},
        detailInfo:{},
        paramInfo:{}
      }
    },
    props: {
    },
    components:{
     DetailNavbar,
     DetailSwiper,
     DetailBaseInfo,
     DetailShopInfo,
    //  Scroll,
     DetailGoodsInfo,
     DetailParamInfo
    },
    created(){
      this.iid=this.$route.params.iid
      getDetail(this.iid).then(res=>{
        // console.log(res)
        const data = res.result
        this.topImages = data.itemInfo.topImages
        this.goods = new Goods(data.itemInfo,data.columns,data.shopInfo.services)
        this.shop = new Shop(data.shopInfo)
        this.detailInfo = data.detailInfo
        this.paramInfo = new GoodsParam(data.itemParams.info,data.itemParams.rule)
      })
    },
    methods:{
      imgLoad(){
        // this.$refs.detail-scroll.refresh()
      }
    }
  }
</script>

<style scoped>
  .detail{
    position: relative;
    z-index: 9;
    background-color: #fff;
    height: 100vh;
  }
  .detail-scroll{
    /* height: calc(100%-44px); */
    position: absolute;
    top: 44px;
    overflow: hidden;
  }
</style>
