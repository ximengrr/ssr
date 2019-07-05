<template>
  <section class="container">
    <!-- 机票标题 -->
    <h1 class="air-title">
      <i class="iconfont iconfeiji"></i>
      <span>国内机票</span>
    </h1>
    <!-- 搜索广告栏 -->
    <el-row class="seatch" type="flex" justify="space-between">
      <!-- 机票搜索 -->
      <el-col>
        <SearchForm></SearchForm>
      </el-col>
      <!-- 广告图片 -->
      <el-col class="sale-banner">
        <img src="../../static/images/pic_sale.jpeg" alt />
      </el-col>
    </el-row>

    <!-- 服务栏 -->
    <el-row type="flex" class="statement" justify="space-around">
      <el-col :span="8">
        <i class="iconfont iconweibiaoti-_huabanfuben" style="color:#409EFF;"></i>
        <span>100%航协认证</span>
      </el-col>
      <el-col :span="8">
        <i class="iconfont iconbaozheng" style="color:green;"></i>
        <span>出航保证</span>
      </el-col>
      <el-col :span="8">
        <i class="iconfont icondianhua" style="color:#409EFF;"></i>
        <span>7x24小时服务</span>
      </el-col>
    </el-row>
    <!-- 特价机票栏 -->
    <el-row type="flex" class="air">
      <h2 class="air-sale-title">
        <span class="iconfont icontejiajipiao"></span>
        <i>特价机票</i>
      </h2>
    </el-row>
    <!-- 特价机票 -->
    <div class="air-sale">
            <el-row type="flex" class="air-sale-pic" justify="space-between">
                <el-col :span="6" v-for="(item, index) in sales" :key="index">
                    <nuxt-link :to="`/air/flights?departCity=${item.departCity}&departCode=${item.departCode}&destCity=${item.destCity}&destCode=${item.destCode}&departDate=${item.departDate}`">
                        <img :src="item.cover"/>
                        <el-row class="layer-bar" type="flex" justify="space-between">
                            <span>{{item.departCity}}-{{item.destCity}}</span>
                            <span>￥699</span>
                        </el-row>
                    </nuxt-link>
                </el-col>
            </el-row>
        </div>
  </section>
</template>

<script>
import Logo from "~/components/Logo.vue";
import SearchForm from "~/components/air/searchForm.vue";
export default {
  components: {
    Logo,
    SearchForm
  },
  data() {
    return {
      sales: [{
                    cover: "https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D220/sign=9154c841bcfd5266a32b3b169b199799/3812b31bb051f8199687c7e0d0b44aed2f73e7fe.jpg",
                    departCity: "广州",
                    departCode: "CAN",
                    departDate: "2019-06-17",
                    destCity: "上海",
                    destCode: "SHA",
                    price: 760
                }]
    };
  },
   mounted(){
        this.$axios({
            url: `/airs/sale`
        }).then(res => {
            this.sales = res.data.data;
        });
    },
};
</script>

<style lang="less" scoped>
.container {
  width: 1000px;
  margin: auto;

  .air-title {
    // height: 40px;
    // line-height: 40px;
    font-weight: normal;
    margin: 15px 0;
    color: orange;
    span {
      font-size: 20px;
    }
    i {
      font-size: 20px;
    }
  }
  .seatch {
    .air-seatch {
      margin-right: 18px;
    }
    .air-banner {
    }
  }
  .statement {
    margin: 15px 0;
    border: 1px #ddd solid;
    background: #f5f5f5;
    height: 58px;
    padding: 10px 0;
    box-sizing: border-box;

    > div {
      text-align: center;
      line-height: 38px;
      border-right: 1px #ddd solid;

      i {
        font-size: 30px;
      }
    }
  }
  .air {
    .air-sale-title {
      i {
        color: rgb(0, 179, 255);
        font-size: 20px;
        font-weight: normal;
      }
    }
  }
  .air-sale {
    border: 1px #ddd solid;
    padding: 20px;
    margin-bottom: 50px;

    .air-sale-pic {
      > div {
        width: 225px;
        height: 140px;
        position: relative;
        overflow: hidden;

        img {
          width: 100%;
        }

        .layer-bar {
          position: absolute;
          bottom: 0;
          left: 0;
          background: rgba(0, 0, 0, 0.5);
          color: #fff;
          height: 30px;
          line-height: 30px;
          width: 100%;
          box-sizing: border-box;
          padding: 0 15px;
          font-size: 14px;

          span:last-child {
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>


