<template>
  <div class="pos">
    <el-row>
      <el-col :span='7' class="pos-order">
        <el-tabs>
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border style="width: 100%" >
              <el-table-column prop="goodsName" label="商品"></el-table-column>
              <el-table-column prop="count" label="数量"></el-table-column>
              <el-table-column prop="price" label="金额"></el-table-column>
              <el-table-column prop="operation" label="操作" width="100" fixed="right">
                <template slot-scope="scope">
                  <el-button type="text" size="small" @click="delGoods(scope.row)">删除</el-button>
                  <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="total">
              <span>数量：{{totalCount}}</span>
              <span>金额：{{totalMoney}}元</span>
            </div>
            <div class="operation-btn">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger" @click="delAllGoods()">删除</el-button>
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
                <li v-for="data in oftenGoods" @click="addOrderList(data)">
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
                   <li v-for="data in type1Goods" @click="addOrderList(data)">
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
                   <li v-for="data in type2Goods" @click="addOrderList(data)">
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
                   <li v-for="data in type3Goods" @click="addOrderList(data)">
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
                    <li v-for="data in type4Goods" @click="addOrderList(data)">
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
        tableData:[],
        oftenGoods:[],
        type1Goods:[],
        type2Goods:[],
        type3Goods:[],
        type4Goods:[],
        totalCount:0,
        totalMoney:0
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

      })
      .catch((error)=> {
        console.log(error);
      });
    },
    mounted(){
      let orderHeight=document.body.clientHeight || document.documentElement.clientHeight;
      document.getElementsByClassName("pos-order")[0].style.height=orderHeight+'px';
    },
    methods:{
      addOrderList(goods){
        this.totalCount=0;
        this.totalMoney=0;
        let isHave=false;
          //判断是否这个商品已经存在于订单列表
        for (let i=0; i<this.tableData.length;i++){
           if(this.tableData[i].goodsId==goods.goodsId){
              isHave=true; //存在
           }
        }
        //根据isHave的值判断订单列表中是否已经有此商品
        if(isHave){
          //存在就进行数量添加
          let arr = this.tableData.filter(o =>o.goodsId == goods.goodsId);
          arr[0].count++;
        }else{
          //不存在就推入数组
          let newGoods={goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
          this.tableData.push(newGoods);
        }

        this.getAllMoney();
      },

      delGoods(goods){
        console.log(goods);
        this.tableData=this.tableData.filter(o => o.goodsId !=goods.goodsId);
        this.getAllMoney();
      },

      delAllGoods() {
        this.tableData = [];
        this.totalCount = 0;
        this.totalMoney = 0;
      },

      //汇总数量和金额
      getAllMoney(){
        this.totalCount = 0;
        this.totalMoney = 0;
        if(this.tableData) {
          this.tableData.forEach((element) => {
          this.totalCount += element.count;
          this.totalMoney = this.totalMoney + (element.price * element.count);
          });
        }
      }
    }
  }
</script>


