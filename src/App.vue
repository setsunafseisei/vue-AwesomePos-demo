<template>
  <div id="app">
    <!--左侧导航-->
    
        <leftNav></leftNav>
    
    <!--操作区域-->
    <div class="main">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import leftNav from "@/components/common/leftNav";

export default {
  name: "App",
  components: {
    leftNav
  }
};
</script>

<style>
#app {
  font-family: "Microsoft YaHei", "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
  margin-top: 0;
}

.main {
  float: left;
  width: 95%;
  height: 100%;
  overflow: auto;
  background-color: #eff2f7;
}
</style>
