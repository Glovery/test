<template>
  <div>
    <el-table :data="tableData" :class="className">
      <el-table-column label="项目名称" prop="projectName"></el-table-column>
      <el-table-column
        label="项目描述"
        prop="desc"
        show-overflow-tooltip
      ></el-table-column>
      <el-table-column
        label="涉及技术"
        prop="skill"
        show-overflow-tooltip
      ></el-table-column>
    </el-table>
  </div>
</template>
<script>
export default {
  props: {
    className: {
      type: String,
      default: "table"
    },
    tableData: {
      type: Array,
      default: () => {
        return [];
      }
    }
  }
};
</script>
<style lang="scss" scoped>
.table {
  width: 600px;
  margin: 0 auto;
}
</style>
