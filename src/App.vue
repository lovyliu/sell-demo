<template>
  <div id="app">
    <Header :seller="seller">

    </Header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link :to="{ name: 'goods', params: {} }">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{ name: 'ratings', params: {} }">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{ name: 'seller', params: {} }">商家</router-link>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
import Header from '@/components/header/header';
const ERR_OK = 0;

export default {
  name: 'App',
  data () {
    return {
      seller: {}
    };
  },
  created () {
    this.$http.get('/api/seller').then((response) => {
      response = response.body;
      if (response.errorno === ERR_OK) {
        this.seller = response.data;
        console.log(this.seller);
      }
    });
  },
  components: {
    Header: Header
  }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"

  .tab
    display:flex
    width: 100%
    height: 40px
    line-height: 40px
    border-1px(rgba(7, 17, 27, 0.1))
    .tab-item
      flex: 1
      text-align: center
      & > a
        display: block
        font-size: 14px
        color: rgb(77,85,93)
        &.active
          color: rgb(240, 20, 20)
</style>
