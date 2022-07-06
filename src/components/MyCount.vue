<template>
  <div class="my-counter">
    <button
      type="button"
      class="btn btn-light"
      @click="goodsObj.goods_count > 1 && goodsObj.goods_count--"
      :disabled="goodsObj.goods_count <= 1"
    >
      -
    </button>
    <input
      type="number"
      class="form-control inp"
      v-model.number="goodsObj.goods_count"
    />
    <button type="button" class="btn btn-light" @click="goodsObj.goods_count++">
      +
    </button>
  </div>
</template>

<script>
export default {
  props: {
    goodsObj: {
      type: Object,
      default: () => ({}),
    },
  },
  watch: {
    goodsObj: {
      deep: true,
      handler(val) {
        if (val.goods_count < 1) {
          val.goodsObj.goods_count = 1;
        }
      },
    },
  },
};
</script>

<style lang="less" scoped>
.my-counter {
  display: flex;
  .inp {
    width: 45px;
    text-align: center;
    margin: 0 10px;
  }
  .btn,
  .inp {
    transform: scale(0.9);
  }
}
</style>
