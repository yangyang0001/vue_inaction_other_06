<template>
    <div class="app-container">
        <Header :title="title"></Header>
        <Goods v-for="goods in list" :key="goods.id" :goods="goods" @change_checked="change_checked"></Goods>
        <Footer :list="list" @all_checked="all_checked"></Footer>
    </div>
</template>

<script>
import axios from 'axios'

import Header from '@/components/header/Header.vue'
import Goods from '@/components/goods/Goods.vue'
import Footer from '@/components/footer/Footer.vue'

import bus from '@/eventBus.js'

export default {
    data() {
        return {
            title: '购物车案例',
            list: []
        }
    },

    created() {
        this.initGoods();
    },

    methods: {
        async initGoods() {
            var result = await axios.get("http://localhost:8888/initGoods")
            /** 页面需要渲染的东西, 理论上都应该在 data 中定义! */
            // console.log(result);
            if (result.status === 200) {
                this.list = result.data;
            }
        },

        change_checked: function (obj) {
            // console.log(obj);
            var id = obj.goods_id;
            var goods_state = obj.goods_state;
            this.list.some((item, index) => {
                if (id === item.id) {
                    this.list[index].goods_state = goods_state;
                    return true;
                }
            })
        },

        all_checked: function (checked) {
            this.list.forEach((item, index) => {
                this.list[index].goods_state = checked;
            });
        }
    },

    mounted() {
        console.log('app.vue mounted');
        var _this = this;
        bus.$on('num_change', function(obj) {
            var id = obj.goods_id;
            var goods_count = obj.goods_count;
            _this.list.some((item, index) => {
                if (id === item.id) {
                    _this.list[index].goods_count = goods_count;
                    return true;
                }
            })
        });
    },

    // 注册组件
    components: {
        Header,
        Goods,
        Footer
    },

}
</script>

<style lang="less" scoped>
.app-container {
    padding-top: 45px;
    padding-bottom: 50px;
}
</style>
