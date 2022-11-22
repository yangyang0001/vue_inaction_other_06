<template>
    <div class="goods-container">
        <!-- 左侧图片区 -->
        <div class="thumb">
            <div class="custom-control custom-checkbox">
                <input type="checkbox" class="custom-control-input" :id="'goods_' + goods.id" :checked="goods.goods_state" 
                @change="change_checked">

                <label class="custom-control-label" :for="'goods_' + goods.id">
                    <img :src="goods.goods_img" alt=""/>
                </label>
            </div>
        </div>
        <!-- 右侧信息区 -->
        <div class="goods-info">
            <!-- 商品标题 -->
            <h6 class="goods-title">{{goods.goods_name}}</h6>
            <div class="goods-info-bottom">
                <!-- 商品价格 -->
                <span class="goods-price">￥{{goods.goods_price}}</span>

                <!-- 商品的数量 -->
                <Counter :goods="goods"></Counter>
            </div>
        </div>
    </div>
</template>

<script>
import Counter from '@/components/counter/Counter.vue'

export default {

    props: {
        goods: {
            default: {},
            type: Object
        }
    },

    data() {
        return {
            
        };
    },

    mounted() {
        
    },

    methods: {
        // 修改勾选状态
        change_checked(e) {
            var param = {
                goods_id : this.goods.id,
                goods_state: e.target.checked
            };
            this.$emit('change_checked', param);
        }
    },

    components: {
        Counter
    }
};
</script>

<style lang="less" scoped>
.goods-container {
  + .goods-container {
    border-top: 1px solid #efefef;
  }
  padding: 10px;
  display: flex;
  .thumb {
    display: flex;
    align-items: center;
    img {
      width: 100px;
      height: 100px;
      margin: 0 10px;
    }
  }

  .goods-info {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;
    .goods-title {
      font-weight: bold;
      font-size: 12px;
    }
    .goods-info-bottom {
      display: flex;
      justify-content: space-between;
      .goods-price {
        font-weight: bold;
        color: red;
        font-size: 13px;
      }
    }
  }
}
</style>