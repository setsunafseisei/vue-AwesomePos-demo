<template>
  <div class="pos">
    <el-row>
      <el-col :span='7' class="pos-order" id="order-list">
        <el-tabs>
          
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border style="width: 100%">

              <el-table-column prop="goodsName" label="商品名称"></el-table-column>
              <el-table-column prop="count" label="数量" width="50"></el-table-column>
              <el-table-column prop="price" label="金额" width="70"></el-table-column>
              <el-table-column label="操作" width="100" fixed="right">
                <template scope="scope">
                    <!-- <el-button type="text" size="small" @click="delSingleGoods(scope.row)">删除</el-button> -->
                    <!-- <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button> -->
                    <el-button type="text" size="small" >删除</el-button>
                    <el-button type="text" size="small" >增加</el-button>

                </template>
              </el-table-column>
              
            </el-table>

            <div class="div-btn">
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

      <el-col :span='17' >
        <div class="often-goods">
          <div class="title">常用商品</div>
          <div class="often-goods-list">
            <ul>
              <li v-for="goods in oftenGoods">
                <span>{{  goods.goodsName }}</span>
                <span class="price">¥ {{ goods.price }}元</span>
              </li>
            </ul>
          </div>
        </div>

        <div class="goodsType">
           <el-tabs>
            <el-tab-pane label="汉堡">
              <div>
                <ul class='cookList'>
                  <li v-for="good in type0Goods">
                      <span class="foodImg"><img :src="good.goodsImg" width="100%"></span>
                      <span class="foodName">{{good.goodsName}}</span>
                      <span class="foodPrice">￥{{good.price}}.00元</span>
                  </li>
              </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="小吃">
              <div>
                <ul class='cookList'>
                  <li v-for="good in type1Goods">
                      <span class="foodImg"><img :src="good.goodsImg" width="100%"></span>
                      <span class="foodName">{{good.goodsName}}</span>
                      <span class="foodPrice">￥{{good.price}}.00元</span>
                  </li>
              </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="饮料">
              <div>
                <ul class='cookList'>
                  <li v-for="good in type2Goods">
                      <span class="foodImg"><img :src="good.goodsImg" width="100%"></span>
                      <span class="foodName">{{good.goodsName}}</span>
                      <span class="foodPrice">￥{{good.price}}.00元</span>
                  </li>
              </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label="套餐">
              <div>
                <ul class='cookList'>
                  <li v-for="good in type3Goods">
                      <span class="foodImg"><img :src="good.goodsImg" width="100%"></span>
                      <span class="foodName">{{good.goodsName}}</span>
                      <span class="foodPrice">￥{{good.price}}.00元</span>
                  </li>
              </ul>
              </div>
            </el-tab-pane>
           </el-tabs>
        </div>
      </el-col>
      <el-col>product column</el-col>
    </el-row>
  </div>
</template>

<script>
import axios from "axios";
// import $ from "jquery"

export default {
  name: "pos",
  data() {
    return {
      tableData: [
        {
          goodsName: "可口可乐",
          price: 8,
          count: 1
        },
        {
          goodsName: "香辣鸡腿堡",
          price: 15,
          count: 1
        },
        {
          goodsName: "爱心薯条",
          price: 8,
          count: 1
        },
        {
          goodsName: "甜筒",
          price: 8,
          count: 1
        }
      ],
      oftenGoods: [],
      type0Goods: [],
      type1Goods: [],
      type2Goods: [],
      type3Goods: []
    };
  },
  // 钩子函数： 创建dom前获取数据（可以通过axios 或 ajax）
  created: function() {
    // axios 获取
    axios
      .get(
        "https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods"
      )
      .then(response => {
        // console.log(response);
        this.oftenGoods = response.data;
      })
      .catch(err => {
        // console.log(err);
        alert("error!");
      });

    // ajax 获取
    // $.get("https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods",function (response) {
    //   console.log(response);
    //   this.oftenGoods = response;
    // })

    axios
      .get(
        "https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods"
      )
      .then(response => {
        this.type0Goods = response.data[0];
        this.type1Goods = response.data[1];
        this.type2Goods = response.data[2];
        this.type3Goods = response.data[3];
      })
      .catch(err => {
        alert("error!");
      });
  },
  mounted: function() {
    var orderHeight = document.body.clientHeight;
    document.getElementById("order-list").style.height = orderHeight + "px";
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pos-order {
  background-color: #f9fafc;
  border-right: #c0ccda 1px solid;
}

.div-btn {
  margin-top: 10px;
}

.title {
  height: 20px;
  border-bottom: #d3dce6 1px solid;
  background-color: #f9fafc;
  padding: 10px;
  text-align: left;
}

.often-goods-list ul li {
  list-style: none;
  float: left;
  border: 1px solid #e5e9f2;
  padding: 10px;
  margin: 10px;
  background-color: #ffffff;
}

.price {
  color: #58b7ff;
}

.goodsType {
  clear: both;
}

.cookList li {
  list-style: none;
  width: 23%;
  border: 1px solid #e5e9f2;
  height: auot;
  overflow: hidden;
  background-color: #fff;
  padding: 2px;
  float: left;
  margin: 2px;
}

.cookList li span {
  display: block;
  float: left;
}
.foodImg {
  width: 40%;
  margin-bottom: -5px;
}
.foodName {
  font-size: 18px;
  padding-left: 10px;
  color: brown;
}
.foodPrice {
  font-size: 16px;
  padding-left: 10px;
  padding-top: 10px;
}
</style>
