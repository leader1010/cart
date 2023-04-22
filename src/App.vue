<template>
  <EsHeader></EsHeader>
  <EsGoods v-for="item in goodslist"
           :key="item.id"
           :id="item.id"
           :thumb="item.goods_img"
           :title="item.goods_name"
           :price="item.goods_price"
           :count="item.goods_count"
           :checked="item.goods_state"
  ></EsGoods>
</template>

<script>
import EsHeader from "./components/es-header/EsHeader.vue";
import EsGoods from "./components/es-goods/EsGoods.vue";

export default {
  name: 'App',
  data() {
    return {
      goodslist: [],
      count: 4
    }
  },
  created() {
    this.getGoodsList()
  },

  props: {},
  methods: {
    // 获取商品列表数据的方法
    async getGoodsList() {
      const {data: res} = await this.$http.get('/api/cart')
      if (res.status !== 200) return alert('数据请求失败！')
      this.goodslist = res.list
    },
  },


  components: {
    EsHeader,
    EsGoods
  },


}
</script>
