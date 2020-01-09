<template>
  <div class="logIn">
    <div class="orientation">
      <Head :title="title" :isBack="isBack" :type="type" :headclass="headclass" class="head"></Head>
      <h3>快捷登录</h3>
      <p>请输入您的手机号和密码</p>
    </div>
    <div class="box">
      <div class="logIn-loading" v-if="loading">
        <cube-loading :size="30"></cube-loading>
      </div>
      
      <div class="main">
        <tab-items></tab-items>
        <!-- <div class="hint">借贷有风险，入市需谨慎</div> -->
      </div>
    </div>
    
  </div>
</template>
<script>
import TabItems from "../../components/TabItems";
import Head from "../../components/head";

import store from "../../store/session";
export default {
  name: "logIn",
  components: {
    Head,
    TabItems
  },
  data() {
    return {
      title: "登录",
      isBack: "",
      loading: true,
      count: 0,
      setInter: "",
      type: "",
      appCode: this.common.wholesituation.appCode,
      session: store.session,
      headclass:true,
    };
  },
  created: function() {
    this.type = this.utils.fetch("type");
    let session = this.utils.fetch("session");
    if (session.length == 0) {
      this.utils.save("session", this.session);
      session = this.session;
    }
    this.setInter = setInterval(this.timer, 200);
  },
  methods: {
    timer: function() {
      if (this.count <= 0) {
        this.count++;
      } else {
        this.loading = false;
        clearInterval(this.setInter);
      }
    }
  }
};
</script>
  <style scoped lang="scss">
  .orientation{
    color: #fff;
    background: url("../../assets/mine_bag.png") no-repeat;
    height:(500)/75 +rem;
    background-size: 100% 100%;
    h3{
      font-size: (68/75)+rem;
      padding-left: (97/75)+rem;
      padding-top: (218/75)+rem;
    }
    p{
      color: #9dcfff;
      font-size: (36/75)+rem;
      padding-left: (97/75)+rem;
      margin-top: (55/75)+rem;
    }
  }
  .head{
    position: absolute;
    top: 0;
    background: none !important;
  }
.logIn-loading {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: #fff;
  z-index: 99999999;
}
img {
  display: block;
  width: 100%;
}
.main {
  padding: 0.2rem 0.6rem 0 0.6rem;
  font-size: 0.2rem;
  .hint {
    font-size: 0.3rem;
    color: #d8d8d8;
    text-align: center;
    margin-top: 1rem;
  }
  .topLogo {
    width: 3.5rem;
    height: 3.5rem;
    margin: 0 auto;
  }
}
</style>