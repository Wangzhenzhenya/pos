<template>
    <div class="pos">
        <el-row>
            <el-col :span="7" class="pos-order" id="order-list">
                <el-tabs style="text-align:center;" type="border-card">
                    <el-tab-pane label="点餐" style="margin-left:0px">
                        <el-table :data="tableDate" border style="width:100%">
                            <el-table-column prop="goodsName" label="商品名称"></el-table-column>
                            <el-table-column prop="count" label="数量" width="50"></el-table-column>
                            <el-table-column prop="price" label="金额" width="70"></el-table-column>
                            <el-table-column  label="操作" width="100" fixed="right">
                                <template slot-scope="scope">
                                    <el-button type="text" size="small" @click="delfoods(scope.row)">删除</el-button>
                                    <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                                </template>
                            </el-table-column>
                        </el-table>
                        <div class='totals'>
                            <small>数量：</small>{{totalsCount}}<small>金额：</small> {{totalsMoney}}元
                        </div>
                        <div class="div-btn">
                            <el-button type="warning">挂单</el-button>
                            <el-button @click="dele" type="danger">删除</el-button>
                            <el-button type="success" @click="checkOut">结账</el-button>
                        </div>
                    </el-tab-pane>

                    <el-tab-pane label="挂单">
                        <el-table>
                            <el-table-column label="name"></el-table-column>
                            <el-table-column label="count"></el-table-column>
                            <el-table-column ></el-table-column>
                        </el-table>
                    </el-tab-pane>
                    <el-tab-pane label="外卖">外卖</el-tab-pane>
                </el-tabs>

            </el-col>
            <el-col :span="17">
                <div class="often-goods">
                    <div class="title">常用商品</div>
                    <div class="often-goods-list">
                        <ul>
                            <li @click="addOrderList(goods)" v-for="(goods, index) in oftenGoods" :key="index">
                                <span>{{goods.goodsName}}</span>
                                <span class="o-price">¥{{goods.price}}元</span>
                            </li>
                        </ul>
                    </div>
                </div>

                <div class="goodsType">
                    <el-tabs>
                        <el-tab-pane label="汉堡">
                            <div>
                                <!-- <ul class='cookList'>
                                    <li @click="addOrderList" v-for="(goods, index) in typeGoods" :key="index">
                                        <span class="foodImg"><img src="goods.goodsImg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul> -->
                                <i class="el-icon-loading"></i>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="小食">
                            <div>
                                <ul class='cookList'>
                                    <li @click="addOrderList(goods)" v-for="(goods, index) in type0Goods" :key="index">
                                        <span class="foodImg"><img src="goods.goodsImg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                                <div class="btnm">
                                    <el-button :plain="true" center @click="open2">成功</el-button>
                                    <el-button :plain="true" @click="open3">警告</el-button>
                                    <el-button :plain="true" @click="open4">消息</el-button>
                                    <el-button :plain="true" @click="open5">错误</el-button>
                                </div>
                                

                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="饮料">
                            <div>
                                <ul class='cookList'>
                                    <li @click="addOrderList(goods)" v-for="(goods, index) in type1Goods" :key="index">
                                        <span class="foodImg"><img src="goods.goodsImg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label="套餐">
                            <div>
                                <ul class='cookList'>
                                    <li @click="addOrderList(goods)" v-for="(goods, index) in type2Goods" :key="index">
                                        <span class="foodImg"><img src="goods.goodsImg" width="100%"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </div>
                        </el-tab-pane>
                    </el-tabs>
                </div>



            </el-col>

        </el-row>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name:'pos',
        data(){
            return {
                tableDate:[{
                    goodsId:9,
                    goodsName: '可口可乐',
                    price: 8,
                    count:1
                    }, {
                    goodsId:1,
                    goodsName: '香辣鸡腿堡',
                    price: 15,
                    count:1
                    }, {
                    goodsId:10,
                    goodsName: '爱心薯条',
                    price: 8,
                    count:1
                    }, {
                    goodsId:11,
                    goodsName: '甜筒',
                    price: 8,
                    count:1
                }],
                oftenGoods:[
                    {
                        goodsId:1,
                        goodsName:'香辣鸡腿堡',
                        price:18
                    }, {
                        goodsId:2,
                        goodsName:'田园鸡腿堡',
                        price:15
                    }, {
                        goodsId:3,
                        goodsName:'和风汉堡',
                        price:15
                    }, {
                        goodsId:4,
                        goodsName:'快乐全家桶',
                        price:80
                    }, {
                        goodsId:5,
                        goodsName:'脆皮炸鸡腿',
                        price:10
                    }, {
                        goodsId:6,
                        goodsName:'魔法鸡块',
                        price:20
                    }, {
                        goodsId:7,
                        goodsName:'可乐大杯',
                        price:10
                    }, {
                        goodsId:8,
                        goodsName:'雪顶咖啡',
                        price:18
                    }, {
                        goodsId:9,
                        goodsName:'大块鸡米花',
                        price:15
                    }, {
                        goodsId:20,
                        goodsName:'香脆鸡柳',
                        price:17
                    }
                ],
                typeGoods:[
                    {
                        goodsId:1,
                        goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1542467201369&di=d3958c28b00a884e4aea30b3f742acba&imgtype=0&src=http%3A%2F%2Fp0.meituan.net%2Fdeal%2F1676944a28bc227047464d6f97a7f5c8152540.jpg",
                        goodsName:'香辣鸡腿堡',
                        price:18
                    }, {
                        goodsId:2,
                        goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1542467201369&di=d3958c28b00a884e4aea30b3f742acba&imgtype=0&src=http%3A%2F%2Fp0.meituan.net%2Fdeal%2F1676944a28bc227047464d6f97a7f5c8152540.jpg",
                        goodsName:'田园鸡腿堡',
                        price:15
                    }, {
                        goodsId:3,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
                        goodsName:'和风汉堡',
                        price:15
                    }, {
                        goodsId:4,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                        goodsName:'快乐全家桶',
                        price:80
                    }, {
                        goodsId:5,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                        goodsName:'脆皮炸鸡腿',
                        price:10
                    }, {
                        goodsId:6,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
                        goodsName:'魔法鸡块',
                        price:20
                    }, {
                        goodsId:7,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
                        goodsName:'可乐大杯',
                        price:10
                    }, {
                        goodsId:8,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                        goodsName:'雪顶咖啡',
                        price:18
                    }, {
                        goodsId:9,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
                        goodsName:'大块鸡米花',
                        price:15
                    }, {
                        goodsId:20,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
                        goodsName:'香脆鸡柳',
                        price:17
                    }
                ],
                type0Goods:[
                    {
                        goodsId:5,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                        goodsName:'脆皮炸鸡腿',
                        price:10
                    }, {
                        goodsId:6,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
                        goodsName:'魔法鸡块',
                        price:20
                    }, {
                        goodsId:7,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
                        goodsName:'可乐大杯',
                        price:10
                    }
                ],
                type1Goods:[
                    {
                        goodsId:1,
                        goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1542467201369&di=d3958c28b00a884e4aea30b3f742acba&imgtype=0&src=http%3A%2F%2Fp0.meituan.net%2Fdeal%2F1676944a28bc227047464d6f97a7f5c8152540.jpg",
                        goodsName:'香辣鸡腿堡',
                        price:18
                    }, {
                        goodsId:2,
                        goodsImg:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1542467201369&di=d3958c28b00a884e4aea30b3f742acba&imgtype=0&src=http%3A%2F%2Fp0.meituan.net%2Fdeal%2F1676944a28bc227047464d6f97a7f5c8152540.jpg",
                        goodsName:'田园鸡腿堡',
                        price:15
                    }, {
                        goodsId:3,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
                        goodsName:'和风汉堡',
                        price:15
                    }
                ],
                type2Goods:[
                    {
                        goodsId:7,
                        goodsName:'可乐大杯',
                        price:10
                    }, {
                        goodsId:8,
                        goodsName:'雪顶咖啡',
                        price:18
                    }, {
                        goodsId:9,
                        goodsName:'大块鸡米花',
                        price:15
                    }, {
                        goodsId:20,
                        goodsName:'香脆鸡柳',
                        price:17
                    }
                ],
                totalsMoney:0,
                totalsCount:0
            }
        },
        mounted:function() {
            var orderheight=document.body.clientHeight;
            document.getElementById('order-list').style.height=orderheight+'px';
            this.tableDate.forEach(element => {
                    this.totalsMoney=this.totalsMoney+(element.price*element.count);
                    this.totalsCount+=element.count;
                });
        },
        methods: {
            open2(){
                this.$message({
                    message:'恭喜你，这是一条成功消息',
                    type:'success'
                });
            },
            open3(){
                this.$message({
                    message:'恭喜你，这是一条警告信息',
                    type:'warning'
                });
            },
            open4(){
                this.$message({
                    message:'恭喜你，这是一条提示信息'
                });
            },
            open5(){
                this.$message({
                    message:'恭喜你，这是一条错误信息',
                    type:'warning'
                });
            },
            dele(){
                this.$confirm('您将删除所有商品，是否继续？','提示',{
                    confirmButtonText:'确定',
                    cancelButton:'取消',
                    type:'warning'
                }).then(()=>{
                    this.tableDate=[];
                    this.totalsMoney=0;
                    this.totalsCount=0;
                    this.$message({
                        type:'success',
                        message:'删除成功！'
                    });
                }).catch(()=>{
                    this.$message({
                        type:'info',
                        message:'已取消删除'
                    });
                });
            },
            addOrderList(goods){
                //商品是否已经存在订单列表
                this.totalsMoney=0;
                this.totalsCount=0;
                let isHave=false;
                for(let i=0;i<this.tableDate.length;i++){
                    if(this.tableDate[i].goodsId==goods.goodsId){
                        isHave=true;
                        break;
                    }
                }
                if(isHave){
                    let arr=this.tableDate.filter(a=>a.goodsId==goods.goodsId);
                    arr[0].count++;
                }else {
                    let newGoods={
                        goodsId:goods.goodsId,
                        goodsName:goods.goodsName,
                        price:goods.price,
                        count:1
                        };
                    this.tableDate.push(newGoods);
                }
                //计算汇总金额和数量
                this.getAllMoney();
            },
            //删除单个商品
            delfoods(goods){
                this.tableDate=this.tableDate.filter(a=>a.goodsId!=goods.goodsId);
                this.getAllMoney();
            },
            getAllMoney(){
                this.totalsCount=0;
                this.totalsMoney=0;
                if(this.tableDate){
                    this.tableDate.forEach(element => {
                    this.totalsMoney=this.totalsMoney+(element.price*element.count);
                    this.totalsCount+=element.count;
                    });
                }
            },
            //模拟结账
           checkOut(){
               if(this.totalsCount!=0){
                   this.tableDate=[];
                   this.totalsMoney=0;
                   this.totalsCount=0;
                   this.$message({
                       message:'结账成功，感谢你又为店里出了一份力',
                       type:'success'
                   })
               }else{
                   this.$message.error('不能空结，老板了解你急切的心情！');
               }
           }
        }
    }
</script>

<style>
.pos-order {
    background-color:#f9fafc;
    border-right: 1px solid #c0ccda;
}
.div-btn {
    margin-top: 10px;
}
.often-goods .title{
    height: 20px;
    border-bottom: 1px solid #d3dce6;
    background-color: #f9fafc;
    padding: 9px;
    text-align: left;
}
.often-goods-list ul li{
    list-style: none;
    float: left;
    border: 1px solid #e5e9f2;
    padding: 10px;
    margin: 10px;
    background-color: #fff;
    cursor: pointer;
}
.totals {
    background-color: #fff;
    padding: 10px;
}
.totals small {
    margin-left: 30px;
}
.o-price {
    color: #58b7ff;
}
.goodsType {
    clear: both;
    padding-left: 9px;
}
.cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auot;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
       cursor: pointer;
   }
   .cookList li span{
        display: block;
        float:left;
   }
   .foodImg{
       width: 40%;
   }
   .foodName{
       font-size: 18px;
       padding-left: 10px;
       color:brown;
   }
   .foodPrice{
       font-size: 16px;
       padding-left: 10px;
       padding-top:10px;
   }
   .btnm{
       float: left;
       margin:20px 0
   }
</style>

