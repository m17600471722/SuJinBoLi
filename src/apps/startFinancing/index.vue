<template>
  <div class="startFinancing">
    <div class="logIn-loading" v-if="loading">
      <cube-loading :size="30"></cube-loading>
    </div>
   <Head :title="title" :isBack="isBack" :isWhite="isWhite"></Head>
    <div class="main">
      <div class="schedule">
        <p class="fin_title">可用额度(元)</p>
        <p class="price">{{price}}</p>
        <div class="progressBar">
          <span @click="addNum"><img src="../../assets/add.png"></span>
          <div class="boc_center">
            <p class="default-theme"></p>
            <p class="default-demo" :style="barStyle"></p>
            <span class="spot" :style="leftStyle"></span>
          </div>
          <span @click="subtract"><img src="../../assets/subtract.png"></span>
        </div>
        <div class="figure">
          <div>
            <p>总额度(元)</p>
            <p>{{totalAmount}}</p>
          </div>
          <div>
            <p>已用额度(元)</p>
            <p>{{hasAmount}}</p>
          </div>
        </div>
        <div class="describe">
          <p class="describe_p1">产品特点</p>
          <p class="rules">1. 只需一张身份证和手机号，就能下款;</p>
          <p class="rules">2. 5分钟审核，30秒下款;</p>
          <p class="rules">3. 不查征信，不打通讯录;</p>
          <p class="rules">4. 利息低致5分钱;</p>
        </div>
      </div>
    </div>
    <div class="applyFor">
      <p class="btn" @click="applyFor">提款申请</p>
    </div>
  </div>
</template>

<script>
import Head from "../../components/head";
import {smallCreditVo,applySmallCreditVo } from "../../api/app.api.js";

export default {
  name: "startFinancing",
  components: {
   Head
  },
  data() {
    return {
      title: "开始融资",
      isBack: "",
      price:0,
      maxprice:0,
      isWhite:2,
      percentage:0,
      percenleft:0,
      totalAmount:0,
      hasAmount:0,
      loading:false,
      num:0,
      oldPrice:0,
      text:"",
      intrada:false
    };
  },
  methods: {
    Totas: function() {
      this.toast = this.$createToast({
        txt: this.text,
        type: "text",
        time: 1000,
        onTimeout: () => {
          if (this.intrada) {
            this.loading = false
            this.$router.push({ name: "home" });
          }
        }
      });
      this.toast.show();
    },
    outLogin(){
      localStorage.clear();
      this.$router.push({ name: "Login" });
    },
    addNum(){ 
      if(this.percentage>=100){
        return
      }
      this.price += 100
      this.percentage += this.num
      this.percenleft += this.num
    },
    subtract(){
      if(this.price<=this.oldPrice){
        return
      }
      this.price -= 100
      this.percentage -= this.num
      this.percenleft -= this.num
    },
    //申请
    applyFor(){
      this.$router.push({ name: "datacenter" });
      // this.loading = true
      // applySmallCreditVo({    
      // })
      // .then(res => {
      //   if (res.code=="200") {
      //     this.intrada = true
      //     this.text = res.message
      //     this.Totas()
      //   }
      // })
      // .catch(error => {
      //   console.log(error);
      // });
    },
    getPrice(){
      smallCreditVo({    
      })
      .then(res => {
        if (res.code=="200") {
          this.totalAmount = parseInt(res.data.totalAmount).toFixed(2)
          this.hasAmount =  parseInt(res.data.hasAmount).toFixed(2)
          this.price = parseInt(res.data.startAmount)
          this.oldPrice = parseInt(res.data.startAmount)
          this.maxprice = parseInt(res.data.avilAmount)
          this.percentage = this.price/this.maxprice*100;
          this.percenleft = this.percentage-1
          this.num = 100/(this.maxprice/100)
          this.loading = false
        }
      })
      .catch(error => {
        console.log(error);
      });
    },
  },
  computed:{
    barStyle() {
      const style = {};
      style.width = this.percentage + '%';
      return style;
    },
    leftStyle(){
      const style = {};
      style.left = this.percenleft + '%';
      return style;
    }
  },
  mounted() {
    this.loading = true
    this.getPrice()
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "./index.scss";
</style>
