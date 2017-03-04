<template>
    <div>
       <h2>购物车详情</h2>
    <el-table :data="cartList" border style="width: 100%">
        <el-table-column label="id" width="180">
            <template scope="scope">
                <el-icon name="time"></el-icon>
                <span style="margin-left: 10px">{{ scope.row.id }}</span>
            </template>
        </el-table-column>
        <el-table-column label="名称" width="180">
            <template scope="scope">
                <el-popover trigger="hover" placement="top">
                    <p>姓名: {{ scope.row.name }}</p>
                    <p>介绍: {{ scope.row.introduce }}</p>
                    <div slot="reference" class="name-wrapper">
                        <el-tag>{{ scope.row.name }}</el-tag>
                    </div>
                </el-popover>
            </template>
        </el-table-column>
        <el-table-column label="价格" width="180">
            <template scope="scope">
                <el-icon name="time"></el-icon>
                <span style="margin-left: 10px">{{ scope.row.price }}</span>
            </template>
        </el-table-column>
        <el-table-column label="数量" width="180">
            <template scope="scope">
                <el-icon name="time"></el-icon>
                <span style="margin-left: 10px">{{ scope.row.num }}</span>
            </template>
        </el-table-column>
        <el-table-column label="总价" width="180">
            <template scope="scope">
                <el-icon name="time"></el-icon>
                <span style="margin-left: 10px">{{ scope.row.price*scope.row.num }}</span>
            </template>
        </el-table-column>
        <el-table-column label="操作">
            <template scope="scope">
                <el-button size="small" @click="action_cart(scope.$index, 'add_db')">+</el-button>
                <el-button size="small" @click="action_cart(scope.$index, 'reduce_db')">-</el-button>
                <el-button size="small" type="danger" @click="action_cart(scope.$index, 'delete_db')">删除</el-button>
            </template>
        </el-table-column>
    </el-table> 
    </div>
    
</template>

<script>
    export default {
        computed: {
            cartList() {
                return this.$store.getters.getCartList;
            }
        },
        methods: {
            /*
            *  购物车加减删操作
            *  @param  {number} index 当前操作的索引
            *  @param  {string} type 对应的mutations值
            *  @param  {string} type=add_db  增加
            *  @param  {string} type=reduce_db  减少
            *  @param  {string} type=delete_db  删除
            */
            action_cart(index, type) {
                //先更新当前索引
                this.$store.dispatch('update_cur_shop_status', {
                    index
                });

                //执行更新state动作
                this.$store.dispatch(type);
            }
        }
    }
</script>