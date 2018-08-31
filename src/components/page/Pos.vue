<template>
  <div class="pos">
    <el-row>
      <el-col :span='7' class="pos-order" id="order-list">
        <el-tabs>
          
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border style="width:100%">
              <el-table-column label="商品名称" props="goodsName"></el-table-column>
              <el-table-column label="数量" props="count" width=50></el-table-column>
              <el-table-column label="价格" props="price" width=70></el-table-column>
              <el-table-column label="操作" width=100 fixed="right">
                <template scope="scope">
                  <el-button type="text" size="small">删除</el-button>
                  <el-button type="text" size="small">增加</el-button>
                </template>
              </el-table-column>
              
            </el-table>
          </el-tab-pane>

          <el-tab-pane label="挂单">
            挂单
          </el-tab-pane>
          <el-tab-pane label="外卖">
            外卖
          </el-tab-pane>
        </el-tabs>
      </el-col>
      <el-col>product column</el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: 'pos',
  data(){
    return {
      tableData:[{
          goodsName: '可口可乐',
          price: 8,
          count:1
        }, {
          goodsName: '香辣鸡腿堡',
          price: 15,
          count:1
        }, {
          goodsName: '爱心薯条',
          price: 8,
          count:1
        }, {
          goodsName: '甜筒',
          price: 8,
          count:1
        }],
    }
  },
  mounted:function(){
    var orderHeight = document.body.clientHeight;
    document.getElementById('order-list').style.height = orderHeight+'px';
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pos-order{
  background-color: #f9fafc;
  border-right:#c0ccda 1px solid;
}
</style>
