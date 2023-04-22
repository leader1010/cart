<template>
  <div class="goods-container">
    <div class="left">
      <!--      <input type="checkbox" name="" id="">-->
      <!--      <img src="" alt="">-->
      <div class="custom-control custom-checkbox">
      <input class="custom-control-input" type="checkbox" value="" :id="id">
      <label class="custom-control-label" :for="id">
        <img :src="thumb" alt="商品图片" class="thumb">
      </label>
      </div>
    </div>


    <div class="right">
      <div class="top">{{title}}111</div>
      <div class="bottom">
        <div class="price">¥{{price}}</div>
        <div class="count">
        </div>


      </div>

    </div>


  </div>
</template>

<script>
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