<template>
    <div>
        <h2>商品详情 </h2>
        <el-table :data="shop_list" border style="width: 100%">
        <el-table-column label="Id" width="180">
            <template scope="scope">
                <span style="margin-left: 10px">{{ scope.row.id }}</span>
            </template>
        </el-table-column>
        <el-table-column label="名称" width="180">
            <template scope="scope">
                <span style="margin-left: 10px">{{ scope.row.name }}</span>
            </template>
        </el-table-column>
        <el-table-column label="姓名" width="180">
            <template scope="scope">
                <el-popover trigger="hover" placement="top">
                    <p>名称: {{ scope.row.name }}</p>
                    <p>简介: {{ scope.row.introduce }}</p>
                    <div slot="reference" class="name-wrapper">
                        <el-tag>{{ scope.row.name }}</el-tag>
                    </div>
                </el-popover>
            </template>
        </el-table-column>
        <el-table-column label="数量" width="180">
            <template scope="scope">
                <span style="margin-left: 10px">{{ scope.row.num || '' }}</span>
            </template>
        </el-table-column>
        <el-table-column label="操作">
            <template scope="scope">
                <el-button size="small" @click="add_db(scope.row)">{{scope.row.num ? '+' : "加入购物车"}}</el-button>
                <el-button size="small" type="danger" @click="reduce_db(scope.row)"  v-if='scope.row.num && scope.row.num>0'>-</el-button>
            </template>
        </el-table-column>
    </el-table>
    </div>
    
</template>

<script>
    export default {
        data() {
            return {
                shop_list: [{
                    id: 1,
                    price: '14',
                    name: '青椒肉丝',
                    num: 0,
                    introduce: '贼拉好吃 啦啦啦啦啦啦啦啦啦啦啦'
                }, {
                    id: 2,
                    price: '16',
                    name: '虎皮辣椒',
                    num: 0,
                    introduce: '贼拉好吃 啦啦啦啦啦啦啦啦啦啦啦'
                }, {
                    id: 3,
                    price: '18',
                    name: '小炒肉',
                    num: 0,
                    introduce: '贼拉好吃 啦啦啦啦啦啦啦啦啦啦啦'
                }, {
                    id: 4,
                    price: '48',
                    name: '臭桂鱼',
                    num: 0,
                    introduce: '贼拉好吃 啦啦啦啦啦啦啦啦啦啦啦'
                }]
            }
        },
        mountd() {
        
            /*
            * 初始化时把购物车的菜品数量绑定到菜品列表中
            */
          let list = this.$store.state.cart.cartList;
          for (let j = 0; j < this.shop_list.length; i++){
              for (var j = 0; j < list.length; j++){
                  if (list[j].id == this.shop_list[i].id){
                      
                      //这种赋值属性的方式，初始化完成时，无法从state同步到列表
                      //this.$set(this.shop_list, i, list[j].num)

                      //通过直接赋值对象，造成对象引用，从而改变state时，达到自动同步列表数据目的
                      this.$set(this.shop_list, i, list[j]);
                      break
                  }
              }
          } 
          console.log(this.shop_list[0].num);
          
        },
        methods: {
            /*
            *  点击菜品列表中的加号
            */
            add_db(shop) {
                let id = shop.id;

                //检测是否存在购物车中，如果存在修改state.curState为true，并设置state，curIndex为当前菜品在购物车中的索引
                this.$store.dispatch('check_db', {
                    id
                })

                //如果存在，先自增当前菜品中的num，再设置购物车的数量
                //如果不存在，直接往购物车中push一个新的菜品
                if (this.$store.state.cart.curIndex != -1){
                    console.log('add_db')
                    this.$store.dispatch('add_db');
                }else {
                    console.log('create_db');
                    this.$set(shop, 'num', 1);
                    this.$store.dispatch('create_db', {
                        shop
                    })
                }
            },
            /*
            *  点击菜品列表中的减号
            */
            reduce_db(shop) {
                let id = shop.id;
                this.$store.dispatch('check_db', {
                    id
                });
                shop.num = parseInt(shop.num);
                this.$store.dispatch('reduce_db');
            }
        }
    }
</script>