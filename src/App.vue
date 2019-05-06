<template>
  <div id="app">
    <!-- 头部 -->
    <mt-header fixed title="黑马程序员·Vue项目"></mt-header>

    <!-- 各种组件 -->
    <router-view/>

    <!-- tabbar -->
    <nav class="mui-bar mui-bar-tab">
      <a class="mui-tab-item mui-active" href="#tabbar">
        <span class="mui-icon mui-icon-home"></span>
        <span class="mui-tab-label">首页</span>
      </a>
      <a class="mui-tab-item" href="#tabbar-with-chat">
        <span class="mui-icon mui-icon-contact"></span>
        <span class="mui-tab-label">会员</span>
      </a>
      <a class="mui-tab-item" href="#tabbar-with-contact">
        <span class="mui-icon mui-icon-extra mui-icon-extra-cart">
          <span class="mui-badge">9</span>
        </span>
        <span class="mui-tab-label">购物车</span>
      </a>
      <a class="mui-tab-item" href="#tabbar-with-map">
        <span class="mui-icon mui-icon-search"></span>

        <span class="mui-tab-label">搜索</span>
      </a>
    </nav>
  </div>
</template>

<script>
export default {
  name: "App"
};
</script>

<style>
</style>
