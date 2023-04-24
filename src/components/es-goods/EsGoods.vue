<template>
  <div class="goods-container">
    <div class="left">
      <!--      <input type="checkbox" name="" id="">-->
      <!--      <img src="" alt="">-->
      <div class="custom-control custom-checkbox">
        <input class="custom-control-input" type="checkbox" :checked="checked" :id="id" @change="onCheckBoxChange">
        <label class="custom-control-label" :for="id">
          <img :src="thumb" alt="商品图片" class="thumb">
        </label>
      </div>
    </div>


    <div class="right">
      <div class="top">{{ title }}111</div>
      <div class="bottom">
        <div class="price">¥{{ price }}</div>
        <div class="count">
        </div>
        <es-counter :num="count" :min="1" @numChange="getNumber"></es-counter>

      </div>

    </div>


  </div>
</template>

<script>
import EsCounter from "../es-counter/EsCounter.vue";

export default {
  name: "EsGoods",
  props: {
    title: {
      type: String
    },
    id: {
      type: [String, Number],

    },

    thumb: {
      type: String
    },

    price: {
      type: Number
    },

    count: {
      type: Number
    },

    checked: {
      type: Boolean,
    }
  },
  emits: ['countChange', 'stateChange'],

  methods: {
    // this 当前组件示例 e.target为触发事件的dom元素
    onCheckBoxChange(e) {
      this.$emit(
          'stateChange', {
            id: this.id,
            value: e.target.checked
          }
      )
    },


    // 监听数量值的变化
    getNumber(num) {
      this.$emit('countChange', {
        id: this.id,
        value: num
      })
    }
  },

  components: {
    EsCounter
  }


}
</script>

<style scoped lang="less">
.goods-container {
  + .goods-container {
    border-top: 1px solid #efefef;
  }

  display: flex;
  padding: 10px;

  // 左侧图片的样式
  .left {
    margin-right: 10px;

    .thumb {
      display: block;
      width: 100px;
      height: 100px;
      background-color: #efefef;
    }
  }

  // 右侧商品名称、单价、数量的样式
  .right {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;

    .top {
      font-weight: bold;
    }

    .bottom {
      display: flex;
      justify-content: space-between;
      align-items: center;

      .price {
        color: red;
        font-weight: bold;
      }
    }
  }
}

.custom-control-label::before,
.custom-control-label::after {
  top: 3.4rem;
}

</style>