<template>
  <div class="pos">
    <el-row>
      <el-col :span='7' class="pos-order" id="order-list">order column</el-col>
      <el-col>product column</el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: 'pos',
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
