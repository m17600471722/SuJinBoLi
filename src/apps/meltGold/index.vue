<template>
  <div class="repayment">
   <Head :title="title" :isBack="isBack" :isWhite="isWhite"></Head>
    <div class="main">
      <img src="../../assets/huankuan.png">
      <p>暂无融资记录~</p>
    </div>
  </div>
</template>

<script>
import Head from "../../components/head";
import { factoringPoolVo } from "../../api/app.api.js";

export default {
  name: "Mine",
  components: {
   Head
  },
  data() {
    return {
      title: "速金融资",
      isBack: "",
      isWhite:2
    };
  },
  methods: {
    //查询
    factoringPoolVo(){
     factoringPoolVo({})
      .then(res => {
        if (res.code == "200") {
          
        } else {
          
        } 
      })
      .catch(error => {
        console.log(error);
      });
    }
  },
  mounted() {
    this.factoringPoolVo()
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "./index.scss";
</style>
