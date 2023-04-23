<template>
  <div class="header">
    {{ title }}
  </div>
</template>

<script>
export default {
  name: "EsHeader",
  props: {
    title: {
      type: String,
      default: '购物车'
    }
  }
}
</script>

<style scoped lang="less">
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 45px;
  text-align: center;
  line-height: 45px;
  background-color: #007BFF;
  z-index: 999;


}
</style>