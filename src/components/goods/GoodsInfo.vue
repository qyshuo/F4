<template>
  <div class="goodsinfo">
    <!-- 轮播图 -->
    <div class="swipe">
      <mt-swipe :show-indicators="false">
        <mt-swipe-item v-for="(v,k) in lunboList" :key="k">
          <img :src="v.img" alt>
        </mt-swipe-item>
      </mt-swipe>
    </div>

    <!-- 购买区域 -->
    <div class="card">
      <div class="card-header">{{infoList.title}}</div>
      <div class="card-content">
        <p class="price">
          市场价：
          <del>￥{{infoList.market_price}}</del>
          &nbsp;&nbsp;销售价：
          <span class="now_price">￥{{ infoList.sell_price }}</span>
          <span></span>
        </p>
        <div class="cont">
          购买数量：
          <div class="mui-numbox" data-numbox-step="10" data-numbox-min="0" data-numbox-max="100">
            <button class="mui-btn mui-numbox-btn-minus" type="button" @click="jiancount()">-</button>
            <input class="mui-numbox-input" type="number" :value="count">
            <button class="mui-btn mui-numbox-btn-plus" type="button" @click="addcount()">+</button>
          </div>
        </div>
        <p>
          <mt-button type="primary">立即购买</mt-button>
          <mt-button type="danger" @click="addshopcard">加入购物车</mt-button>
        </p>
      </div>
    </div>

    <!-- 商品参数 -->
    <div class="card">
      <div class="card-header">商品参数</div>
      <div class="card-content">
        <p>商品货号：{{ infoList.goods_no }}</p>
        <p>库存情况：{{ infoList.stock_quantity }}件</p>
        <p>上架时间：{{ infoList.add_time }}</p>
      </div>
      <div class="card-foot">
        <mt-button type="primary" size="large" plain>图文介绍</mt-button>
        <mt-button type="danger" size="large" plain>商品评论</mt-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  created() {
    this.getlunboList();
    this.getinfoList();
  },
  mounted() {
    
  },
  methods: {
    async getlunboList() {
      const { data: dt } = await this.$http.get("api/getthumimages/" + this.id);
      // console.log(dt)
      dt.message.forEach(item => {
        item.img = item.src;
      });
      this.lunboList = dt.message;
    },
    async getinfoList() {
      const { data: dt } = await this.$http.get("api/goods/getinfo/" + this.id);
      // console.log(dt);
      this.infoList = dt.message[0];
    },
    addcount(){
      this.count++
    },
    jiancount(){
      if(this.count<=1){
        return this.count=1
      }
      this.count-- 
    },
    addshopcard(){
      var goodsinfo = {
        id:this.id,
        price:this.infoList.sell_price,
        count:this.count
      }
      window.localStorage.setItem('goods',goodsinfo.count)
      // this.$emit('togoods',goodsinfo)
      // console.log(goodsinfo)
      this.$router.go(0)
    }
  },
  data() {
    return {
      id: this.$route.params.id,
      lunboList: [],
      infoList: [],
      count:1
    };
  }
};
</script>

<style >
.goodsinfo {
  padding-bottom: 50px;
}
.swipe {
  width: 100%;
  height: 230px;
}
.mint-swipe {
  margin: 10px;
  background: #fff;
}
.mint-swipe-item {
  padding: 15px;
  text-align: center;
}
img {
  display: inline-block;
  width: 200px;
  height: 200px;
}
.card {
  margin: 10px;
  background-color: #fff;
}
.card-header {
  font-size: 17px;
  padding: 10px 15px;
  border-bottom: 1px solid #ccc;
}
.card-content {
  padding: 15px;
}
.now_price {
  color: red;
  font-size: 16px;
  font-weight: bold;
}
.cont{
  margin: 10px;
}
.card-foot {
  border-top: 1px solid #ccc;
  padding: 20px;
}
.mint-button {
  margin-bottom: 10px;
}
</style>
