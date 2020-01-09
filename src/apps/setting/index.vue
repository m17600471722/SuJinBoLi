<template>
  <div class="setting">
   <Head :title="title" :isBack="isBack" :isWhite="isWhite"></Head>
    <div class="box main_box" @click="aboutLink">
      <p>关于我们</p>
      <img src="../../assets/right.png">
    </div>
    <div class="main_box">
      <div class="box versions">
        <p>当前版本</p>
        <span>1.1.1</span>
      </div>
      <div class="box">
        <p>清除缓存</p>
        <span>0.67MB</span>
      </div>
    </div>
    <div class="main_box">
      <div class="btn" @click="outLogin">退出登录</div>
    </div>
  </div>
</template>

<script>
import Head from "../../components/head";
import { } from "../../api/app.api.js";

export default {
  name: "Mine",
  components: {
   Head
  },
  data() {
    return {
      title: "设置",
      isBack: "",
      isWhite:1
    };
  },
  methods: {
    outLogin(){
      localStorage.clear();
      this.$router.push({ name: "Login" });
    },
    aboutLink(){
      this.$router.push({ name: "about" });
    }
  },
  mounted() {
  
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "./index.scss";
</style>
