<template>
    <div class="footer-container">
        <!-- 左侧的全选 -->
        <div class="custom-control custom-checkbox">
            <input type="checkbox" class="custom-control-input" id="goodsFull" :checked="selectAll"
                @change="all_checked" />
            <label class="custom-control-label" for="goodsFull">全选</label>
        </div>

        <!-- 中间的合计 -->
        <div>
            <span>合计：</span>
            <span class="total-price">￥{{ amount.toFixed(2) }}</span>
        </div>

        <!-- 结算按钮 -->
        <button type="button" class="btn btn-primary btn-settle">
            结算（{{ allNum }}）
        </button>
    </div>
</template>

<script>
export default {

    props: {
        list: {
            type: Array,
            default: []
        }
    },

    data() {
        return {

        };
    },

    mounted() {

    },

    computed: {
        selectAll: function () {
            return this.list.every(item => item.goods_state === true);
        },

        allNum: function () {
            var allNum = 0;
            this.list.filter(item => item.goods_state === true).forEach(item => {
                allNum += item.goods_count;
            });
            return allNum;
        },

        amount: function () {
            var prices = 0;
            this.list.filter(item => item.goods_state === true).forEach(item => {
                prices += item.goods_price * item.goods_count;
            });
            return prices;
        }
    },

    methods: {
        all_checked(e) {
            this.$emit('all_checked', e.target.checked);
        }
    },
};
</script>

<style lang="less" scoped>
.footer-container {
    font-size: 12px;
    height: 50px;
    width: 100%;
    border-top: 1px solid #efefef;
    position: fixed;
    bottom: 0;
    background-color: #fff;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 10px;
}

.custom-checkbox {
    display: flex;
    align-items: center;
}

#goodsFull {
    margin-right: 5px;
}

.btn-settle {
    height: 80%;
    min-width: 110px;
    border-radius: 25px;
    font-size: 12px;
}

.total-price {
    font-weight: bold;
    font-size: 14px;
    color: red;
}
</style>