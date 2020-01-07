<template>
  <div class="home">
    <header class="header">
      
      <van-swipe :autoplay="3000" indicator-color="white">
        <van-swipe-item><img src="../../assets/home1.png" alt=""></van-swipe-item>
        <van-swipe-item><img src="../../assets/home2.jpg" alt=""></van-swipe-item>
        <van-swipe-item><img src="../../assets/home3.jpg" alt=""></van-swipe-item>
      <van-swipe-item><img src="../../assets/home4.jpg" alt=""></van-swipe-item>
</van-swipe>
    </header>
    <!-- 内容部分 -->
    <van-notice-bar
    text="临近年货节，我们商城将会上架一系列新图书，敬请期待"
    left-icon="volume-o"
/>
    <div>
      <!-- 栏目6个 -->
      <van-grid :column-num="3">
        <van-grid-item
        v-for="value in categories"
        :key="value.id"
        :icon="value.icon"
        :text="value.name"
        />
      </van-grid>
      <!-- 产品4个 -->
      <van-grid :column-num="2" icon-size="350px">
        <briup-product-item v-for="p in products" :key="p.id" :data="p" @click="toBuyHandler(p)"></briup-product-item>
      </van-grid>
    </div>
  </div>
</template>
<script>
import {get,post} from '../../http/axios';

export default {
  methods:{
    //加载栏目信息
    localCategories(){
      let url = "/category/findAll";
      get(url).then((response)=>{
        //将查询结果，数组中的前6个
        this.categories=response.data.slice(0,6);
      })
    },
    //加载产品信息
    localProducts(){
      let url = "/product/query"
      let params = {
        page:0,
        pageSize:10
      }
      post(url,params).then((response)=>{
        this.products = response.data.list;
      })
    },
    toBuyHandler(p){
      this.$router.push({
        path:"/manager/order_confirm",
        query:p
      })
    }
  },
  data(){
    return{
      categories:[],
      products:[]
    }
  },
  created(){
    //查询栏目
    this.localCategories();
    //查询产品
    this.localProducts();
  }
}
</script>
<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 170px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
</style>
