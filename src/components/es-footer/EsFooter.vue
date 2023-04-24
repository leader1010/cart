<template>
  <div class="footer-container">
    <!-- 全选区域 -->
    <div class="all-select">
      <input type="checkbox" name="" id="all-select" @change="onCheckBoxChange" :checked="isFull">
      <label for="all-select">全选</label>
    </div>

    <!-- 合计区域 -->
    <div>
      <span>合计: </span>
      <span class="amount">¥{{ amount.toFixed(2) }}</span>
    </div>

    <!-- 结算按钮 -->
    <button type="button" class="btn btn-primary btn-settle" :disabled="total === 0">结算（{{ total }}）</button>


  </div>
</template>

<script>
export default {
  name: "EsFooter",
  props: {
    amount: {
      type: Number,
      default: 0
    },

    total: {
      type: Number,
      default: 0
    },

    isFull: {
      type: Boolean,
      default: false
    }

  },
  emits: ['fullChange'],
  methods: {
    onCheckBoxChange(e) {
      this.$emit('fullChange', e.target.checked)
    }
  }


}
</script>

<style scoped lang="less">
.footer-container {
  position: fixed;
  bottom: 0;
  left: 0;
  display: flex;
  height: 50px;
  width: 100%;
  background-color: #fff;
  border-top: 1px solid #efefef;
  justify-content: space-between;
  align-items: center;
  align-content: center;
  padding: 0 10px;

  .all-select {
    input {
      display: inline-block;
      border-radius: 50%;
    }
  }

  .amount {
    font-weight: bold;
    color: red;
  }

  .btn {
    min-width: 90px;
    height: 38px;
    border-radius: 19px;
  }
}


</style>