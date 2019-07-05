<template>
  <div class="container">
    <!-- 轮播图 -->
    <div class="banner-big">
      <!-- <span class>默认 Hover 指示器触发</span> -->
      <el-carousel :interval="2000" arrow="always" height="700px">
        <el-carousel-item v-for="(item,index ) in banners" :key="index">
          <div
            class="banner-image"
            :style="
        `background:url(${$axios.defaults.baseURL + item.url})center center no-repeat ;
        background-size:contain contain`
        "
          ></div>
        </el-carousel-item>
      </el-carousel>
    </div>
    <!-- 搜索框 -->
    <div class="banner-content">
      <div class="search-bar">
        <!-- tab栏 -->
        <el-row type="flex" class="search-tab">
          <span
            v-for="(item,index) in options"
            :key="index"
            @click="handleOption(index)"
            :class="{active:index===currentOption}"
          >
            <i>{{item.name}}</i>
          </span>
        </el-row>
        <!-- 输入框 -->
        <el-row type="flex" align="middle" class="search-input">
          <input
            type="text"
            class="search-input-title"
            :placeholder="options[currentOption].placeholder"
            @keydown.enter="handleSearch"
            v-model="searchValue"
            clearable
          />
          <i class="el-icon-search" @click="handleSearch"></i>
        </el-row>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";

export default {
  components: {
    Logo
  },
  data() {
    return {
      // 轮播图数据
      banners: [],
      // tab栏的数据
      options: [
        // 搜索框tab选项
        {
          name: "攻略",
          placeholder: "请输入搜索城市",
          pageUrl: "/travel?city="
        },
        {
          name: "酒店",
          placeholder: "请输入搜索城市搜索酒店",
          pageUrl: "/hotel?city="
        },
        {
          name: "机票",
          placeholder: "请输入出发城市",
          pageUrl: "/air"
        }
      ],
      searchValue: "", //搜索框的值
      currentOption: 0 // 当前选中的选项,index
    };
  },
  methods: {
    // 切换tab栏时候触发
    handleOption(index) {
      console.log(index);
      this.currentOption = index;

      // 如果切换的机票tab，那么直接跳转到几机票页面
      const item = this.options[index];
      if (item.name === "机票") {
        // return this.$router.push(item.pageUrl);
        return this.$router.push(item.pageUrl );
      }
    },
    handleSearch() {
      // console.log( options);
      const item = this.options[this.currentOption];
      return this.$router.push(item.pageUrl + this.searchValue);
    }
  },

  mounted() {
    // Vue.prototype.$axios = axios
    // nuxt或默认把axios绑定到组件的原型，每个组件实例通过this.$axios来调用
    this.$axios({
      url: "/scenics/banners"
    }).then(res => {
      console.log(res);
      const { data } = res.data;
      this.banners = data;
    });
  }
};
</script>
<style lang="less" scoped>
.container {
  margin: 0 auto;
  min-width: 1000px;
  position: relative;
  /* 轮播图部分样式 */
  .banner-big {
    height: 700px;
    .banner-image {
      width: 100%;
      height: 100%;
    }
  }
  // 搜索框部分样式
  .banner-content {
    z-index: 9;
    width: 1000px;
    position: absolute;
    left: 50%;
    top: 40%;
    margin-left: -500px;
    // border-top: transparent solid;
    .search-bar {
      margin: 0 auto;
      width: 552px;
      .search-tab {
        .active {
          i {
            color: #333;
          }
          &::after {
            background: aqua;
          }
        }
        span {
          width: 86px;
          height: 36px;
          display: block;
          margin-right: 8px;
          cursor: pointer;
          position: relative;

          i {
            position: absolute;
            z-index: 2;
            display: block;
            font-size: 18px;
            width: 100%;
            height: 100%;
            line-height: 30px;
            text-align: center;
            color: #fff;
          }
          &:after {
            position: absolute;
            left: 0;
            top: 0;
            display: block;
            content: "";
            width: 100%;
            height: 100%;
            border: 1px rgba(255, 255, 255, 0.2) solid;
            border-bottom: none;
            transform: scale(1.1, 1.3) perspective(0.7em) rotateX(2.2deg);
            transform-origin: bottom left;
            background: rgba(0, 0, 0, 0.5);
            border-radius: 1px 2px 0 0;
            box-sizing: border-box;
          }
        }
      }
      .search-input {
        width: 552px;
        //  height: 100%;
        background: #fff;
        border-radius: 0 5px 5px 5px;
        border: 1px rgba(255, 255, 255, 0.2) solid;
        border-top: none;
        box-sizing: unset;
         input {
          // border-radius: 0 0 0 5px;
          border: none;
          outline: none;
          flex: 1;
          padding: 13px 15px; 
          font-size: 16px;
          box-sizing: border-box;
        }

        .el-icon-search {
          font-size: 20px;
          cursor: pointer;
          font-weight: bold;
        }
      }
    }
  }
}
</style>
