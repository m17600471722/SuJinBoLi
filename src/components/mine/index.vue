<template>
  <div class="me">
    <div class="menu" v-for="data in item" v-if="!data.hidde" @click="menuLink(data)">
      <p class="icon">
        <img v-if="data.path==1" src="../../assets/pay1.png" />
        <img v-if="data.path==2" src="../../assets/pay2.png" />
        <img v-if="data.path==3" src="../../assets/service-icon.png" />
        <img v-if="data.path==4" src="../../assets/set.png" />
        {{data.name}}
      </p>
      <p class="rightIcon" v-if="data.path==4">
        <img src="../../assets/right.png" />
      </p>
      <p class="rightIcon" v-if="data.path!=4">
        {{data.content}}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "me",
  props: ["item", "status"],
  data() {
    return {
      text: "",
      totalType: "",
      intrada: false
    };
  },
  methods: {
    Totas: function() {
      this.toast = this.$createToast({
        txt: this.text,
        type: this.totalType,
        time: 1000,
        onTimeout: () => {
          if (this.intrada) {
            this.$router.push({ name: "Login" });
          }
        }
      });
      this.toast.show();
    },
    menuLink: function(way) {
      // var token = (this.token = this.utils.fetch("token"));
      if(way.linkName != ""){
        this.$router.push({
          name: way.linkName,
          query: { status: this.status, way: way.linkName }
        });
      }
      // if (token.length == 0) {
      //   this.intrada = true;
      //   this.text = "未登录，请登录";
      //   this.Totas();
      // } else {
      //   if (way.linkName === "aboutM") {
      //     return
      //   } else if (token.length <= 0) {
      //     this.$router.push({ name: "Login" });
      //   } else {
      //     this.$router.push({
      //       name: way.linkName,
      //       query: { status: this.status, way: way.linkName }
      //     });
      //   }
      // }
    }
  },
  mounted() {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.menu {
  display: flex;
  justify-content: space-between;
  padding: 0.25rem 0;
  font-size: 0.4rem;
  line-height: 1rem;
  background: #fff;
  img {
    width: 0.3rem;
  }
  .rightIcon {
    display: flex;
    align-items: center;
    color: #BEC6CE ;
  }
}
.menu:last-child{
  border-bottom: 0;
}
.icon {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  color: #6f7275;
  img {
    width: 0.5rem;
    align-items: center;
    margin-right: 0.2rem;
  }
}
</style>
