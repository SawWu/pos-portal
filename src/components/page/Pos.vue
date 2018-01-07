<template>
  <div class="pos">
    <el-row>
      <el-col :span='7' class="pos-order">
        <el-tabs>
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border show-summary style="width: 100%" >
              <el-table-column prop="goodsName" label="商品"></el-table-column>
              <el-table-column prop="count" label="数量"></el-table-column>
              <el-table-column prop="price" label="金额"></el-table-column>
              <el-table-column prop="operation" label="操作" width="100" fixed="right">
                <template slot-scope="scope">
                   <el-button type="text" size="small">删除</el-button>
                   <el-button type="text" size="small">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="operation-btn">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger">删除</el-button>
              <el-button type="success">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单">
            挂单
          </el-tab-pane>
          <el-tab-pane label="外卖">
            外卖
          </el-tab-pane>
        </el-tabs>
      </el-col>
      <el-col :span="17">
          <div class="often-goods">
            <div class="title">常用商品</div>
            <div class="often-goods-list">
                <ul>
                    <li v-for="data in oftenGoods">
                        <span v-text="data.goodsName"></span>
                        <span class="o-price">￥{{data.price}}元</span>
                    </li>
                </ul>
            </div>
          </div>
          <div class="goods-type">
             <el-tabs>
               <el-tab-pane label="汉堡">
                 <ul class='cookList'>
                   <li v-for="data in typeGoods">
                     <span class="foodImg"><img src="http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg" width="100%"></span>
                     <span class="foodName" v-text="data.goodsName"></span>
                     <span class="foodPrice">￥{{data.price}}元</span>
                   </li>
                 </ul>
               </el-tab-pane>
               <el-tab-pane label="小食"></el-tab-pane>
               <el-tab-pane label="饮料"></el-tab-pane>
               <el-tab-pane label="套餐"></el-tab-pane>
             </el-tabs>
          </div>
      </el-col>
    </el-row>
  </div>
</template>
<style lang="less">
  @import "../../assets/less/pos.less";
</style>
<script>
  export default {
    name: 'pos',
    mounted:function(){
       let orderHeight=document.body.clientHeight || document.documentElement.clientHeight;
       document.getElementsByClassName("pos-order")[0].style.height=orderHeight+'px';
    },
    data () {
      return {
        tableData:
        [{
          goodsName: '可口可乐',
          price: 8,
          count:1
        },{
          goodsName: '香辣鸡腿堡',
          price: 15,
          count:1
        },{
          goodsName: '爱心薯条',
          price: 8,
          count:1
        },{
          goodsName: '甜筒',
          rice: 8,
          count:1
        }],
        oftenGoods:
        [{
          goodsId:1,
           goodsName:'香辣鸡腿堡',
           price:18
        },{
           goodsId:2,
           goodsName:'田园鸡腿堡',
           price:15
        },{
           goodsId:3,
           goodsName:'和风汉堡',
           price:15
        },{
           goodsId:4,
           goodsName:'快乐全家桶',
           price:80
        }, {
            goodsId: 5,
            goodsName: '脆皮炸鸡腿',
            price: 10
        },{
           goodsId:6,
           goodsName:'魔法鸡块',
           price:20
        },{
           goodsId:7,
           goodsName:'可乐大杯',
           price:10
        },{
           goodsId:8,
           goodsName:'雪顶咖啡',
           price:18
        },{
           goodsId:9,
           goodsName:'大块鸡米花',
           price:15
        },{
           goodsId:20,
           goodsName:'香脆鸡柳',
           price:17
        }],
        typeGoods:
        [{
          goodsId:1,
          goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
          goodsName:'香辣鸡腿堡',
          price:18
        },{
                goodsId:2,
                goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
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
        }]
      }
    }
  }
</script>


