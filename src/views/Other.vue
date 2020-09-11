<template>
  <div class="other">
    <my-bar :width="width" :seriesData="seriesData" v-if="flag"></my-bar>
    <my-table :tableData="tableData" v-else></my-table>
  </div>
</template>

<script>
import MyBar from "@/components/MyBar";
import MyTable from "@/components/MyTable";
export default {
  components: {
    MyBar,
    MyTable
  },
  data() {
    return {
      width: "400px",
      timer: null,
      flag: false,
      seriesData: [],
      tableData: []
    };
  },
  watch: {
    flag(val) {
      if (val) {
        this.getBarData();
      } else {
        this.getTable();
      }
    }
  },
  mounted() {
    this.getTable();
    this.coumputedShow();
  },
  methods: {
    getBarData() {
      this.$http.get("../../data.json").then(res => {
        if (res.data.code === 200) {
          this.seriesData = res.data.y;
        }
      });
    },
    getTable() {
      this.$http.get("../../project.json").then(res => {
        if (res.data.code === 200) {
          this.tableData = res.data.data;
        }
      });
    },
    coumputedShow() {
      this.timer = null;
      clearInterval(this.timer);
      this.timer = setInterval(() => {
        this.flag = !this.flag;
      }, 10000);
    }
  }
};
</script>
<style lang="scss" scoped>
.other {
  width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
