<template>
  <div class="about">
    <my-table :tableData="tableData"></my-table>
  </div>
</template>
<script>
import MyTable from "@/components/MyTable";
export default {
  name: "about",
  components: {
    MyTable
  },
  created() {
    this.init();
  },
  data() {
    return {
      tableData: []
    };
  },
  methods: {
    init() {
      this.getTable();
    },
    getTable() {
      this.$http.get("../../project.json").then(res => {
        if (res.data.code === 200) {
          this.tableData = res.data.data;
        }
      });
    }
  }
};
</script>
<style lang="scss" scoped>
.about {
  width: 1200px;
  margin: 0 auto;
}
</style>
