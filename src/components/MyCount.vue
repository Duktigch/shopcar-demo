<template>
  <div class="my-counter">
    <button type="button" class="btn btn-light" :disabled="obj.goods_count === 1" @click="obj.goods_count--">-</button>
    <input type="number" class="form-control inp" v-model.number="obj.goods_count">
    <button type="button" class="btn btn-light" @click="obj.goods_count++">+</button>
  </div>
</template>

<!-- 目标：实现商品数量改变
      1.外部传入数据对象obj
      2.v-model关联对象的goods_count的属性和输入框
      3.实现商品+或-，使商品不得小于1（通过输入框和-按钮的禁止）
      4.侦听数量的改变，小于1 直接覆盖1
 -->
<script>
export default {
  props: {
    obj: Object
  },
  watch: {
    obj: {
      deep: true,
      handler() {    // 当商品数量改变的时候，执行handler方法
        if(this.obj.goods_count < 1) {
          this.obj.goods_count = 1
        }
      }
    }
  }
}
</script>

<style lang="less" scoped>
.my-counter {
  display: flex;
  .inp {
    width: 45px;
    text-align: center;
    margin: 0 10px;
  }
  .btn, .inp{
    transform: scale(0.9);
  }
}
</style>