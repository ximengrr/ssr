<template>
  <el-row type="flex" class="container" >
    酒店首页
    <div id="container"></div>
  </el-row>
</template>

<script>
import Logo from "~/components/Logo.vue";

export default {
  components: {
    Logo
  },
  mounted() {
    window.onLoad = function() {
      var map = new AMap.Map("container", {
        zoom: 11, //级别
        center: [116.397428, 39.90923], //中心点坐标
        viewMode: "3D" //使用3D视图
      });
         
    };
    var key="e45f035666485e0c5effb2bcc10b59a9";
    var url =`https://webapi.amap.com/maps?v=1.4.15&key=${key}&callback=onLoad`;
    var jsapi = document.createElement("script");
    jsapi.charset = "utf-8";
    jsapi.src = url;
    document.head.appendChild(jsapi);
  }
};
</script>

<style lang="less" scoped>
#container {
  height: 400px;
  width: 400px;
 justify-content: space-between;
}
</style>

