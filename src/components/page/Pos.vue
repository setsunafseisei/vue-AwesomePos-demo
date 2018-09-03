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
                    <!-- scope.row  当前行数据 scope表示当前作用域 -->
                    <el-button type="text" size="small" @click="delGood(scope.row)">删除</el-button>
                    <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>

                </template>
              </el-table-column>
              
            </el-table>

            <div class="totalDiv">
              <small>数量：</small> {{totalCount}}　　　<small>金额：</small> {{totalMoney}} <small>元</small>
            </div>

            <div class="div-btn">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger" @click="delAllGoods">删除订单</el-button>
              <el-button type="success" @click="checkOut">结账</el-button>
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
              <li v-for="goods in oftenGoods" @click="addOrderList(goods)">
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
                  <li v-for="good in type0Goods" @click="addOrderList(good)">
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
                  <li v-for="good in type1Goods" @click="addOrderList(good)">
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
                  <li v-for="good in type2Goods" @click="addOrderList(good)">
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
                  <li v-for="good in type3Goods" @click="addOrderList(good)">
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
      tableData: [],
      oftenGoods: [],
      type0Goods: [],
      type1Goods: [],
      type2Goods: [],
      type3Goods: [],
      totalMoney: 0,
      totalCount: 0
    };
  },
  // 钩子函数： 创建dom前获取数据（可以通过axios 或 ajax）
  created: function() {
    /*
    // fetch 获取(fetch 学习地址 ：https://segmentfault.com/a/1190000011433064)
    fetch("https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods", { // 在URL中写上传递的参数
      method: 'GET'
    })
    .then((res)=>{
      return res.json()
    })
    .then((res)=>{
      console.log(res)
      this.oftenGoods = res;
    })*/

    /*
    // ajax 获取
    $.get("https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods",function (response) {
      console.log(response);
      this.oftenGoods = response;
    })
    */

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
  },
  // 绑定方法 实现用数据驱动dom
  methods: {

    // 增加 商品 到 结算列表
    addOrderList(good) {
      this.totalMoney = 0;
      this.totalCount = 0;

      // 商品是否 已经 存在于订单列表中
      let isHave = false; // 默认不存在
      for (let i = 0; i < this.tableData.length; i++) {
        if (this.tableData[i].goodsId == good.goodsId) {
          isHave = true;
        }
      }

      // 若已经有该产品 则不新增 而是修改数量
      if (isHave == true) {
        // 已有 增加数量
        let arr = this.tableData.filter(o => o.goodsId == good.goodsId); // filter() 按内部方法条件过滤数据（留下满足内部方法的） 返回为一个数组
        arr[0].count++;
      } else {
        // 没有 新增一条
        let newGood = {
          goodsId: good.goodsId,
          goodsName: good.goodsName,
          price: good.price,
          count: 1
        };

        this.tableData.push(newGood);
      }

      this.getAllMonAndCount();

    },

    // 删除单个商品
    // delGood(good) {
    //   this.tableData = this.tableData.filter(o => o.goodsId != good.goodsId);
    //   this.getAllMonAndCount();
    // },
    delGood(good) {

      if (good.count>1) {
        good.count --;
      } else {
        this.tableData = this.tableData.filter(o => o.goodsId != good.goodsId);
      }
      
      this.getAllMonAndCount();
    },

    // 删除全部商品
    delAllGoods(){
      this.tableData = [];
      this.totalMoney = 0;
      this.totalCount = 0;
    },

    // 总金额和总数量计算
    getAllMonAndCount() {
      this.totalMoney = 0;
      this.totalCount = 0;
      if (this.tableData) {
        this.tableData.forEach(element => {
          // console.log(element);
          this.totalMoney += element.price * element.count;
          this.totalCount += element.count;
        });
      }
    },

    // 模拟结账
    checkOut(){
      if (this.totalCount != 0) {
        
        this.delAllGoods()// 清空所有数据

        // this.$message({
        //   message:"结账成功！",
        //   type:'success',
        //   duration:800,
        //   showClose: true,
        // });
      } else {
        // this.$message.error("当前未选中商品") // 不可设置时间
        this.$message({
          message:"当前未选中商品",
          type:'warning',
          duration:800,
          showClose: true,
        });
      }
    },
    
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
  cursor: pointer;
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
  cursor: pointer;
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
  font-size: 16px;
  padding-left: 10px;
  color: brown;
}
.foodPrice {
  font-size: 16px;
  padding-left: 10px;
  padding-top: 10px;
}

.totalDiv {
  background-color: #fff;
  padding: 10px;
  border-bottom: 1px solid #d3dce6;
}
</style>
