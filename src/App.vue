<template>
  <div>
    <MyHeader title="我的购物车" background="hotpink" color="white" />
    <div class="main">
      <MyGoods v-for="item in list" :key="item.id" :goodsObj="item" />
    </div>
    <MyFooter @changeAll="all"></MyFooter>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue';
import MyGoods from './components/MyGoods.vue';
import MyFooter from './components/MyFooter.vue';
// 目标: 项目初始化 - 静态页面
// 1. 创建项目, 下包, 引入bs样式
// 2. 拆分需求组件, 创建 - 分别标签+样式
// 3. App.vue上显示, 微调样式(上下内边距)

// 目标: 数据 铺设到MyGoods组件上
// 1. 数据在data保存一下(页面只能用data里值)
// 2. 页面v-for循环MyGoods组件
// 3. 分别传入obj数据对象 (一对一关系)
// 4. 内部使用数据对象值渲染到标签上

export default {
  data() {
    return {
      list: [],
    };
  },
  methods: {
    all(val) {
      this.list.forEach((obj) => (obj.goods_state = val));
    },
  },
  created() {
    this.$axios({
      url: '/api/cart',
    }).then((res) => {
      this.list = res.data.list;
    });
  },
  components: {
    MyHeader,
    MyGoods,
    MyFooter,
  },
};
</script>

<style scoped>
.main {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
