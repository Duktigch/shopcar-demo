<template>
  <!-- 底部 -->
  <div class="my-footer">
    <!-- 全选 -->
    <div class="custom-control custom-checkbox">
      <input type="checkbox" class="custom-control-input" id="footerCheck" v-model="isAll">
      <label class="custom-control-label" for="footerCheck">全选</label>
    </div>
    <!-- 合计 -->
    <div>
      <span>合计:</span>
      <span class="price">¥ {{ allPrice }}</span>
    </div>
    <!-- 按钮 -->
    <button type="button" class="footer-btn btn btn-primary">结算 ( {{ allCount }} )</button>
  </div>
</template>


<!-- 目标：全选
  1.先给全选按钮绑定计算完整属性
  2.set获取全选的状态->子传父this.$emit->父亲操作forEach->影响其它小选框的状态
  3.get给全选返回状态->父传子小选框状态props->get内操作every->影响全选状态
 -->
<script>
export default {
  props:['arr'],
  computed: {
    isAll: {
      set(val) {
        this.$emit('changeAll', val)
      },
      get() {
        return this.arr.every(obj => obj.goods_state === true)
      }
    },
    allCount(){
      return this.arr.reduce((sum, obj) => {
          if (obj.goods_state === true) { // 选中商品才累加数量
              sum += obj.goods_count;
          }
          return sum;
      }, 0)
    },
    allPrice() {
      return this.arr.reduce((sum, obj) => {
        if(obj.goods_state === true) {
          sum += obj.goods_count * obj.goods_price
        }
        return sum
      }, 0)
    }
  }
}
</script>

<style lang="less" scoped>
.my-footer {
  position: fixed;
  z-index: 2;
  bottom: 0;
  width: 100%;
  height: 50px;
  border-top: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 10px;
  background: #fff;

  .price {
    color: red;
    font-weight: bold;
    font-size: 15px;
  }
  .footer-btn {
    min-width: 80px;
    height: 30px;
    line-height: 30px;
    border-radius: 25px;
    padding: 0;
  }
}
</style>