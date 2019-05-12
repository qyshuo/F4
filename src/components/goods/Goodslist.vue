<template>
  <div class="goods-list">
    <div class="goods-item" v-for="v in goodlist" :key="v.id" @click="goDetail(v.id)">
      <!-- <router-link :to="'/goodsinfo/'+v.id"> -->
      <img :src="v.img_url" alt>
      <h1 class="title">{{v.title}}</h1>
      <div class="info">
        <p class="price">
          <span class="now">￥{{v.sell_price}}</span>
          <span class="old">￥{{v.market_price}}</span>
        </p>
        <p class="sell">
          <span>热卖中</span>
          <span>剩{{v.stock_quantity}}件</span>
        </p>
        
      </div>
      <!-- <router-link> -->
    </div>
    
    <mt-button type="danger" size="large" @click="getMore">加载更多</mt-button>
  </div>
</template>

<script>
import { Toast } from 'mint-ui';
export default {
  created(){
    this.getGoodsList()
  },
  methods: {
    async getGoodsList(){
      const {data:dt} = await this.$http.get('/api/getgoods?pageindex='+ this.pageindex)
      console.log(dt)
      if(dt.status!==0){
        Toast('获取数据失败');
      }
      // this.goodlist= dt.message
      this.goodlist =this.goodlist.concat(dt.message) 
    },

    getMore(){
      this.pageindex++
      this.getGoodsList()
    },
    goDetail(id){
      // this.$router.push("/goodsinfo"+id);
      this.$router.push({ name: "goodsinfo", params: { id } });
    }
  },
  data() {
    return {
      pageindex: 1,
      goodlist:[]
    };
  }
};
</script>

<style >
.goods-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 7px;
  margin-bottom: 50px;
}
.goods-item {
  width: 49%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  border:1px solid #ccc;
  margin: 4px 0;
  background: #fff;
}
img {
  width: 100%;
}
.title {
  font-size: 14px;
}
.info{
    background-color: #eee;
}
p{
    margin: 0;
    padding: 5px;
}
.now{
    color:red;
    font-size: 16px;
    font-weight: 700;
}
.old{
    text-decoration: line-through;
    font-size: 12px;
    margin-left: 10px;
}
.sell {
        display: flex;
        justify-content: space-between;
        font-size: 13px;
        color: blue;
}
</style>
