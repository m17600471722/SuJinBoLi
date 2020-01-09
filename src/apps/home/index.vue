<template>
  <div class="home_box" >
    <div class="main">
      <div class="title">
        <span></span>
        <p>速金保理</p>
        <img @click="linkMy" src="../../assets/home/more.png">
      </div>
      <div class="company">
        <p>企业名称</p>
        <p>{{companyName}}</p>
      </div>
      <div class="figure">
        <div>
          <p>可用金额(元)</p>
          <p>{{avilAmount}}</p>
        </div>
        <div>
          <p>申请中(元)</p>
          <p>{{applyAmount}}</p>
        </div>
        <div>
          <p>已提现额度(元)</p>
          <p>{{hasAmount}}</p>
        </div>
      </div>
    </div>
    <div class="financing">
      <div @click="linkPage('startFinancing')">
        <img src="../../assets/home/home1.png">
        <p>开始融资</p>
      </div>
      <div @click="linkPage('meltGold')">
        <img src="../../assets/home/home2.png">
        <p>速金融资</p>
      </div>
      <div @click="linkPage('repayment')">
        <img src="../../assets/home/home3.png">
        <p>我要还款</p>
      </div>
    </div>
    
  </div>
</template>
<script>
import { myInfoVo } from "../../api/app.api";;
export default {
  name: "home",
  data() {
    return {
      token:"",
      text:"",
      companyName:"",
      applyAmount:"",
      avilAmount:"",
      hasAmount:""
    };
  },
  methods: {
    Totas: function() {
      this.toast = this.$createToast({
        txt: this.text,
        type: "text",
        time: 1000,
      });
      this.toast.show();
    },
    linkMy(){
      this.$router.push({ name: "Mine" });
    },
    linkPage(nameLink){
      if(nameLink != undefined && nameLink != ""){
        this.$router.push({ name:  nameLink});
      }else{
        this.text = "敬请期待！"
        this.Totas()
      }      
    },
    myinfo(){
     myInfoVo({})
      .then(res => {
        if (res.code == "200") {
          this.utils.save("homedata", res.data);
          this.companyName = res.data.companyName
          this.applyAmount = res.data.applyAmount
          this.avilAmount = res.data.avilAmount
          this.hasAmount = res.data.hasAmount
        } else {
          this.text = res.msg;
          this.Totas();
        } 
      })
      .catch(error => {
        console.log(error);
      });
    }
  },
  mounted() {
    this.token = this.utils.fetch("token");
    if (this.token.length == 0||this.token==undefined) {
      this.$router.push({ name: "Login" });
    }else{
      this.myinfo()
    }
  }
};
</script>
<style lang='scss' scoped>
@import "./index.scss";

</style>