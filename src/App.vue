<template>
  <div>
    <MyHeader background="blue" color="#ccc" title="购物车"></MyHeader>
    <div class="main">
      <MyGoods v-for="obj in list" :key="obj.id" :obj="obj"></MyGoods>
    </div>
    <MyFooter @changeAll="allFn" :arr="list"></MyFooter>
  </div>
</template>


<!-- 项目初始化：
  1.创建项目，下包，引入样式
  2.创建组件
  3.引入组件
  4.注册组件
  5.将注册名->对应模板中
 -->
<script>
import MyFooter from './components/MyFooter.vue'
import MyGoods from './components/MyGoods.vue'
import MyHeader from './components/MyHeader.vue'

export default {
  components: {
    // MyFooter: MyFooter es6规定，组件名和注册名一致可以简化
    MyFooter,
    MyGoods,
    MyHeader
  },
  name: 'WorkspaceJsonApp',

  data() {
    return {
      list: [] // 商品所有数据
    };
  },
  created() {
    this.$axios({
      url: "/api/cart"
    }).then(res => {
      console.log(res);
      this.list = res.data.list
    }).catch((e) => {})
  },
  methods: {
    allFn(val) {
      return this.list.forEach(obj=>obj.goods_state = val)
    }
  }
};
</script>

<style scoped>
  .main {
    padding-top: 45px;
    padding-bottom: 50px;
  }
</style>