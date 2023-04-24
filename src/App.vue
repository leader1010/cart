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
           @countChange="onGoodsCountChange"
           @stateChange="onGoodsStateChange"
  ></EsGoods>
  <EsFooter @fullChange="onFullStateChange" :total="total" :amount="amount"></EsFooter>
</template>

<script>
import EsHeader from "./components/es-header/EsHeader.vue";
import EsGoods from "./components/es-goods/EsGoods.vue";
import EsFooter from "./components/es-footer/EsFooter.vue";

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

    // 监听选中状态变化的事件 全选
    onFullStateChange(isFull) {
      this.goodslist.forEach(x => (x.goods_state = isFull))
    },

    // 监听商品数量变化的事件
    onGoodsCountChange(e) {
      const findResult = this.goodslist.find(x => x.id === e.id)
      if (findResult) {
        // e.value 表示当前文本输入框的值，是在触发 numChange  事件时通过 $emit 方法传递给父组件的一个参数。
        findResult.goods_count = e.value
      }
    },

    onGoodsStateChange(e) {
      const findResult = this.goodslist.find(x => x.id === e.id)
      if (findResult) {
        findResult.goods_state = e.value
      }
    }
  },
  computed: {
    // 已勾选商品的总价格
    amount() {
      let a = 0
      this.goodslist
          .filter(x => x.goods_state)
          .forEach(x => {
            a += x.goods_price * x.goods_count
          })

      return a
    },
    // 已勾选商品的总数量
    total() {
      let t = 0
      this.goodslist
          .filter(x => x.goods_state)
          .forEach(x => {
            t += x.goods_count
          })
      return t
    },


  },


  components: {
    EsHeader,
    EsGoods,
    EsFooter
  },


}
</script>
