<template>
  <div class="repayment">
   <Head :title="title" :isBack="isBack" :isWhite="isWhite"></Head>
    <div class="main">
      <img src="../../assets/huankuan.png">
      <p>您当前还没有还款计划~</p>
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
      title: "我要还款",
      isBack: "",
      isWhite:2
    };
  },
  methods: {
    outLogin(){
      localStorage.clear();
      this.$router.push({ name: "Login" });
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
