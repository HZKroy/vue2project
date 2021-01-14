<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
  import BS from 'better-scroll'
  export default {
    name: 'Scroll',
    data(){
      return {
        scroll:null
      }
    },
    props: {
      probeType:{
        type:Number,
        default(){
          return 0
        }
      },
      pullUpLoad:{
        type: Boolean,
        default(){
          return false
        }
      }
    },
    components:{
    },
    mounted(){
      this.scroll = new BS(this.$refs.wrapper,{
        click:true,
        probeType:this.probeType,
        pullUpLoad:this.pullUpLoad
      })
      if(this.probeType === 2 || this.probeType === 3){
        this.scroll.on('scroll',(position) => {
        // console.log(position)
        this.$emit('scroll',position)
      })
      }
      if(this.pullUpLoad){
        this.scroll.on('pullingUp',() => {
        // console.log('上拉加载更多')
        this.$emit('pullingUp')
        })
      }
    },
    methods:{
      scrollTo(x,y,time=300){
        this.scroll && this.scroll.scrollTo(x,y,time)
      },
      refresh(){
        this.scroll && this.scroll.refresh()
        // console.log('--')
      },
      finishPullUp(){
        this.scroll && this.scroll.finishPullUp()
      }
    }
  }
</script>

<style scoped>
  .wrapper{
    overflow: hidden;
  }
</style>
