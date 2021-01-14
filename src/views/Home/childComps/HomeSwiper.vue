<template>
  <div id="homeSwiper">
    <swiper>
      <swiper-item v-for="item in banners" :key="item.value">
        <a :href="item.link">
          <img :src="item.image" alt="">
        </a>
      </swiper-item>
      <!-- <swiper-item>
        <a :href="banners[0].link">
          <img :src="banners[0].image" alt="">
        </a>
      </swiper-item>
      <swiper-item>
        <a :href="banners[1].link">
          <img :src="banners[1].image" alt="">
        </a>
      </swiper-item> -->
    </swiper>
  </div>
</template>

<script>
  import {Swiper,SwiperItem} from 'components/common/swiper'

  export default {
    name: 'HomeSwiper',
    props: {
      banners:{
        type:Array,
        default(){
          return []
        }
      }
    },
    components:{
      Swiper,
      SwiperItem
    }
  }
</script>

<style scoped>

</style>
