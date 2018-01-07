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
                   <li v-for="data in type1Goods">
                     <span class="foodImg">
                         <img :src="data.goodsImg" width="100%" />
                     </span>
                     <span class="foodName" v-text="data.goodsName"></span>
                     <span class="foodPrice">￥{{data.price}}元</span>
                   </li>
                 </ul>
               </el-tab-pane>
               <el-tab-pane label="小食">
                 <ul class='cookList'>
                   <li v-for="data in type2Goods">
                     <span class="foodImg">
                       <img :src="data.goodsImg" width="100%" />
                     </span>
                     <span class="foodName" v-text="data.goodsName"></span>
                     <span class="foodPrice">￥{{data.price}}元</span>
                   </li>
                 </ul>
               </el-tab-pane>
               <el-tab-pane label="饮料">
                 <ul class='cookList'>
                   <li v-for="data in type3Goods">
                     <span class="foodImg">
                       <img :src="data.goodsImg" width="100%" />
                     </span>
                     <span class="foodName" v-text="data.goodsName"></span>
                     <span class="foodPrice">￥{{data.price}}元</span>
                   </li>
                 </ul>
               </el-tab-pane>
               <el-tab-pane label="套餐">
                 <ul class='cookList'>
                    <li v-for="data in type4Goods">
                      <span class="foodImg">
                        <img :src="data.goodsImg" width="100%" />
                      </span>
                      <span class="foodName" v-text="data.goodsName"></span>
                      <span class="foodPrice">￥{{data.price}}元</span>
                    </li>
                 </ul>
               </el-tab-pane>
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
  import axios from 'axios'
  export default {
    name: 'pos',
    data () {
      return {
        tableData: [{
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
        oftenGoods:[],
        type1Goods:[],
        type2Goods:[],
        type3Goods:[],
        type4Goods:[],
      }
    },
    created(){
      axios.get('http://jspang.com/DemoApi/oftenGoods.php')
      .then((response)=> {
        this.oftenGoods=response.data;
      })
      .catch((error)=> {
         console.log(error);
      });

      axios.get('http://jspang.com/DemoApi/typeGoods.php')
      .then((response)=> {
        this.type1Goods=response.data[0];
        this.type2Goods=response.data[1];
        this.type3Goods=response.data[2];
        this.type4Goods=response.data[3];
        console.log(response);
      })
      .catch((error)=> {
        console.log(error);
      });
    },
    mounted(){
      let orderHeight=document.body.clientHeight || document.documentElement.clientHeight;
      document.getElementsByClassName("pos-order")[0].style.height=orderHeight+'px';
    }
  }
</script>


