<template>
  <div id="cateGory">
    <h3>Category</h3>
    <div class="wrapper">
      <ul class="content">
        <li>a1</li>
        <li>a2</li>
        <li>a3</li>
        <li>a4</li>
        <li>a5</li>
        <li>a6</li>
        <li>a7</li>
        <li>a8</li>
        <li>a9</li>
        <li>a10</li>
        <li>a11</li>
        <li>a12</li>
        <li>a13</li>
        <li>a14</li>
        <li>a15</li>
        <li>a16</li>
        <li>a17</li>
        <li>a18</li>
        <li>a19</li>
        <li>a20</li>
        <li>a21</li>
        <li>a22</li>
        <li>a23</li>
        <li>a24</li>
        <li>a25</li>
        <li>a26</li>
        <li>a27</li>
        <li>a28</li>
        <li>a29</li>
        <li>a30</li>
        <li>a31</li>
        <li>a32</li>
        <li>a33</li>
        <li>a34</li>
        <li>a35</li>
        <li>a36</li>
        <li>a37</li>
        <li>a38</li>
        <li>a39</li>
        <li>a40</li>
        <li>a41</li>
        <li>a42</li>
        <li>a43</li>
        <li>a44</li>
        <li>a45</li>
        <li>a46</li>
        <li>a47</li>
        <li>a48</li>
        <li>a49</li>
        <li>a50</li>
      </ul>
    </div>
    
  </div>
</template>

<script>
  import BS from 'better-scroll'
  export default {
    name: 'Category',
    data(){
      return {
        // scroll:null
      }
    },
    props: {
    },
    components:{
    },
    mounted(){
      let bs = new BS(document.querySelector('.wrapper'),{
        probeType:3,
        pullUpLoad:true,
      })
      bs.on('scroll',(position) => {
        // console.log(position)
      })
      bs.on('pullingUp',() => {
        console.log('pullingUp')
        setTimeout(() => {
          bs.finishPullUp()
        },1000)
      })
    }
  }
  </script>

<style scoped>
  .wrapper{
    height: 500px;
    background-color: red;
    /* overflow-y: scroll; */
  }
</style>
