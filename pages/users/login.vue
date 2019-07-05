<template>
  <div class="container">
    <!-- 主要内容 -->
    <el-row type="flex" rules class="main">
      <div class="form-wrapper">
        <!-- 表单头部tab -->
        <el-row type="flex" class="tabs">
          <span
            v-for="(item ,index) in options"
            :class="{active:currentTab===index}"
            :key="index"
            @click="handleChangeTab(index)"
          >{{item}}</span>
        </el-row>
        <!-- 引入表单栏 -->
        <LoginForm v-if="currentTab===0" />
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <!-- 引入註冊表單欄 -->
        <RegisterForm v-else />
      </div>
    </el-row>
  </div>
</template>
 
<script>
import Logo from "~/components/Logo.vue";
import LoginForm from "~/components/user/loginForm.vue";
import RegisterForm from "~/components/user/registerForm.vue";
export default {
  components: {
    Logo,
    LoginForm,
    RegisterForm
  },
  data() {
    return {
      options: ["登录", "注册"],
      currentTab: 0
    };
  },
  methods: {
    handleChangeTab(index) {
      console.log(index);
      this.currentTab = index;
    }
  }
};
</script>

<style lang="less" scoped>
.container {
  background: url(http://157.122.54.189:9095/assets/images/th03.jfif) center;
  min-width: 1000px;
  height: 700px;
  .main {
    height: 100%;
    width: 400px;
    margin: 0 auto;
    position: relative;
    // line-height:350px;
    display: block;
    .form-wrapper {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 400px;
      // height: 50px;
      background: #fff;
      box-shadow: 2px 2px 0 rgba(0, 0, 0, 0.1);
      overflow: hidden;

      .tabs {
        justify-content: center;
        > span {
          display: block;
          width: 50%;
          height: 50px;
          box-sizing: border-box;
          border-top: 2px #eee solid;
          background: #eee;
          text-align: center;
          line-height: 48px;
          cursor: pointer;
          color: #666;
        }
        .active {
          color: orange;
          background: #fff;
          border-top-color: orange;
          font-weight: bold;
        }
      }
    }
  }
}
</style>