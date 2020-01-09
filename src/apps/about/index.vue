<template>
  <div class="logIn">
    <div class="logIn-loading" v-if="loading">
      <cube-loading :size="30"></cube-loading>
    </div>
    <Head :title="title" :isBack="isBack" :isWhite="isWhite"></Head>
    <div class="main">
      <p>{{aboutHtml}}</p>
    </div>
  </div>
</template>

<script>
import Head from "../../components/head";
import {aboutWo } from "../../api/app.api.js";

export default {
  name: "Mine",
  components: {
    Head,
  },
  created() {

  },
  data() {
    return {
      title: "关于我们",
      isBack: "",
      isWhite:1,
      loading:false,
      aboutHtml:""
    };
  },
  methods: {
    about(){
      aboutWo({})
      .then(res => {
        this.loading = false
        if (res.code == "200") {
          this.aboutHtml = res.data
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
    this.loading = true
    this.about()
  },
};
</script>

<style scoped lang="scss">
@import "./index.scss";
</style>
