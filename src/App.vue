<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
      <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
      <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>
<script>
 import header from './components/header/header.vue';

 const ERR_OK = 0;
 export default {
  data() {
    return {
      seller: {}
    };
  },
  created() {
    this.$http.get('/api/seller').then((response) => {
      response = response.body; // 转为json对象
      if (response.errno === ERR_OK) {
        this.seller = response.data;
        // console.log(this.seller);
      }
    });
  },
  components: {
    'v-header': header
  }
};
</script>
<style>
  .tab{
    display: flex;
    width: 100%;height: 40px;line-height: 40px;
    /* 1px 像素问题 */
    position: relative;
  }
  /* 1px 像素问题 */
  .tab:after{
    position: absolute;display: block;left: 0;bottom: 0;width: 100%;border-top: 1px solid rgba(7,17,27,0.1);content: ' ';
  }

  .tab .tab-item{
    flex: 1;text-align: center;
  }
  .tab .tab-item a{
    display: block; font-size: 14px; color: rgb(77,85,93);
  }
  .tab .tab-item .active{
    color: rgb(220,20,20);
  }
</style>
