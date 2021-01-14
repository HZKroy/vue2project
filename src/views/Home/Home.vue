<template>
  <div id="home">
    <navbar class="home-navbar">
      <div slot="center">购物街</div>
    </navbar>
    <scroll class="scroll" ref="scroll" :probe-type="3" :pull-up-load="true" @scroll="scroll" @pullingUp="pullingUp">
      <home-swiper :banners="banners"></home-swiper>
      <recommend-view :recommends="recommends"></recommend-view>
      <feature-view></feature-view>
      <tab-control ref="tabControl" :titles="['流行','新款','精选']" @tabClick="tabClick"></tab-control>
      <goods-list :goods="goods[currentType].list"></goods-list>
    </scroll>
    <back-top @click.native="backTopClick" v-show="isShowBackTop"></back-top>
  </div>
</template>

<script>

  import Scroll from 'components/common/scroll/Scroll'
  import Navbar from 'components/common/navbar/Navbar'
  import TabControl from 'components/content/tabControl/TabControl'
  import GoodsList from 'components/content/goods/GoodsList'
  import BackTop from 'components/content/backTop/BackTop'

  import HomeSwiper from 'views/Home/childComps/HomeSwiper'
  import RecommendView from 'views/Home/childComps/RecommendView'
  import FeatureView from 'views/Home/childComps/FeatureView'
  

  import {getHomeMultidata,getHomeGoods} from 'network/home'
  import {debounce} from 'common/utils'


  export default {
    name: 'Home',
    data(){
      return {
        banners:[],
        recommends:[],
        goods:{
          'pop':{page:0,list:[]},
          'new':{page:0,list:[]},
          'sell':{page:0,list:[]},
        },
        currentType:'pop',
        isShowBackTop:false,
        tabOffsetTop:0
      }
    },
    props: {
    },
    components:{
      Navbar,
      TabControl,
      HomeSwiper,
      RecommendView,
      FeatureView,
      GoodsList,
      Scroll,
      BackTop,
    },
    methods:{
      //轮播图及推荐数据
      getHomeMultidataM(){
        getHomeMultidata().then(res => {
          // console.log(res)
          this.banners = res.data.banner.list
          this.recommends = res.data.recommend.list
        })
      },
      //商品数据
      getHomeGoodsM(type){
        let page=this.goods[type].page+1
        getHomeGoods(type,page).then(res => {
          // console.log(res)
          this.goods[type].list.push(...res.data.list)
          this.goods[type].page += 1

          this.$refs.scroll.finishPullUp()
        })
      },
      //商品tabbar点击切换
      tabClick(index){
        switch(index){
          case 0:
            this.currentType = 'pop'
            break
          case 1:
            this.currentType = 'new'
            break
          case 2:
            this.currentType = 'sell'
            break
        }
      },
      //监听回到顶部按钮的点击
      backTopClick(){
        this.$refs.scroll && this.$refs.scroll.scrollTo(0,0,500)
      },
      //监听scroll滚动数据传递
      scroll(position){
        // console.log(position)
        this.isShowBackTop = -position.y>1000
      },
      //监听子组件发射的上拉加载
      pullingUp(){
        // console.log("上拉加载")
        this.getHomeGoodsM(this.currentType)
        this.$refs.scroll.refresh()
      }
    },   
    created(){
      this.getHomeMultidataM()
      this.getHomeGoodsM('pop')
      this.getHomeGoodsM('new')
      this.getHomeGoodsM('sell')
    },
    mounted(){
      const refreshDe = debounce(this.$refs.scroll.refresh,800)
      //监听每个小组件的图片加载完成
      this.$bus.$on('ItemImgLoad',() => {
        refreshDe()
      })
      //获取tabControl的offset
      this.tabOffsetTop = this.$refs.tabControl.$el.offsetTop
    }
  }
</script>

<style scoped>
  #home{
    padding-top: 44px;
    height: 100vh;
    position: relative;
  }
  .home-navbar{
    background-color: rgb(219, 26, 116);
    color: white;
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 10;
  }
  .scroll{
    overflow: hidden;
    position: absolute;
    top: 44px;
    bottom: 49px;
  }
  
</style>