<template>
    <div class="cart-info">
        <div>
            <div class="item">
                总数：<strong>{{cartInfos.total_nums}}</strong>
            </div>
            <div class="item">
                总价：<strong>{{cartInfos.total_price}}</strong>
            </div>
            <el-button size="small" type="danger" @click="clear_db">清空购物车</el-button>
        </div>
    </div>
</template>

<script>
    export default {
        computed: {
            cartInfos() {
                return this.$store.getters.getInfos;
            }
        },
        methods: {
            clear_db() {
                this.$store.dispatch('clear_local')
            }
        }
    }
</script>

<!--<style scoped lang="scss">
    .cart-info{
        font-size: 20px; text-align: center;
        .item{
            display: inline-block; margin-right: 20px;
        }
    }
</style>-->