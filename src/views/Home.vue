<template>
  <div>
    <div class="container">
    <Banner :swiperSlides="slider" />
    <div>
      <ul class="homelist">

        <li v-for="item in homelist"
            :key="item.id">
          <img :src="item.img"
               alt="">
          <p>{{item.name}}</p>
        </li>
      </ul>
    </div>
    </div>
  </div>
</template>
<script>
import Banner from "../components/Banner";
// import * as obj from "../api";
// console.log(obj)
// console.log(obj.getBanner.toString())
import { getHomeAll} from  '../api'
console.log(getHomeAll)
export default {
  name: "home",
  created() {
    // ajax 异步 越早发送越好 一般放 created
    this.getAll();
  
  },
  data() {
    return {
      slider: [],
      homelist: []
    };
  },
  components: {
    Banner
  },
  methods: {
   async getAll(){
     let [{banner},{list}] =await getHomeAll();
     this.slider = banner;
     this.homelist = list;
   }
  }
};
</script>
<style>
    .homelist{
      display:flex;
      flex-wrap: wrap;
    }
    .homelist li{
      width: 50%;
      display: flex;
      justify-content: center;
      flex-direction: column;
    }
    .homelist li img{
      width: 90%;
     border-radius: 5px;;
    }
</style>