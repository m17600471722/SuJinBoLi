<template>
  <div>
    <div :class="{head:true,headclass:headclass,bagBlue:isWhite==2}">
      <div class="head_left" @click="goback">
        <img v-if="isWhite==1" src="../../assets/head/black.png">
        <img v-else src="../../assets/head/goback.png" />
      </div>
      <div class="head_center">{{title}}</div>
      <div class="head_right"></div>
    </div>
    <div class="head_lucency"></div>
  </div>
</template>

<script>
import { linkSync } from "fs";
//import { mapState, mapActions } from 'vuex'
export default {
  name: "me",
  props: ["title", "isBack", "isUser", "type","headclass","isWhite"],
  data() {
    return {};
  },
  methods: {
    goback: function() {
      if (this.isBack == "") {
        this.$router.goBack();
      } else if (this.isUser == "") {
        this.$router.push({ name: "Login" });
      } else if (this.type == "Mine") {
        this.$router.push({ name: "Mine" });
      } else if (this.type == "datacenter") {
        this.$router.push({ name: "Mine" });
      } else {
        this.$router.push({ name: "home" });
      }
    }
  },
  mounted() {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.head {
  display: flex;
  justify-content: space-between;
  height: 1.17rem;
  align-items: center;
  font-size: 0.45rem;
  position: fixed;
  width: 100%;
  background: #fff;
  z-index: 999;
  color: #000;
}
.bagBlue{
  background: #3CA0FF ;
  color: #fff;
}
.headclass{
  background: none;
}
.head_lucency {
  height: 1rem;
  padding: 0 10px;
}
.head_left,
.head_right {
  width: 0.6rem;
}
.head_left{
  padding-left: 10px;
}
.head_left img{
 width: 0.3rem;
 height: 0.5rem;
}
</style>
