<template>
  <div class="home">
    <div class="container">
      <h3 class="title">个人简历</h3>
      <h4 class="item-title">个人资料</h4>
      <ul class="content">
        <li v-for="(val, name, index) in personInfo" :key="index" class="item">
          {{ name }}:{{ val }}
        </li>
      </ul>
      <h4 class="item-title">专业技能</h4>
      <p v-for="(item, index) in skillArray" :key="index" class="txt">
        {{ item }}；
      </p>
    </div>
    <my-bar :width="width" :seriesData="seriesData" ref="echarts"></my-bar>
  </div>
</template>

<script>
// @ is an alias to /src
import MyBar from "@/components/MyBar";
export default {
  name: "Home",
  components: {
    MyBar
  },
  mounted() {
    this.getPersonData();
  },
  data() {
    return {
      width: "400px",
      personInfo: {},
      skillArray: [],
      seriesData: []
    };
  },
  methods: {
    getPersonData() {
      this.$http.get("../../data.json").then(res => {
        if (res.data.code === 200) {
          this.personInfo = res.data.data;
          this.skillArray = res.data.skill;
          this.seriesData = res.data.y;
        }
      });
    }
  }
};
</script>
<style lang="scss" scoped>
.home {
  width: 1200px;
  margin: 0 auto;
  display: flex;
  .container {
    width: 800px;
    .item-title {
      padding: 0 50px;
      box-sizing: border-box;
      text-align: left;
    }
    .content {
      padding: 0 50px;
      margin-bottom: 15px;
      display: flex;
      justify-content: center;
      flex-flow: row wrap;
      .item {
        list-style-type: none;
        text-align: left;
        width: 50%;
        margin-top: 10px;
      }
    }
    .txt {
      text-align: left;
      padding: 0 60px;
      position: relative;
      margin: 5px 0;
      &::before {
        position: absolute;
        left: 45px;
        top: 8px;
        content: "";
        width: 8px;
        height: 8px;
        border-radius: 50%;
        background-color: #000;
      }
    }
  }
}
</style>
