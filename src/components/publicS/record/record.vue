  <template>
  <div id="record">
    <el-table
      :data="tableData"
      style="width: 100%"
      :height="heig"
      @selection-change="handleSelectionChange"
      :header-cell-style="{
        background: '#dddddd',
        color: '#606266',
        textAlign: 'center',
        fontSize: '14px',
      }"
      :cell-style="{ padding: '5px', textAlign: 'center', fontSize: '12px' }"
    >
      <slot name="start"></slot>
      <el-table-column
        v-for="(item, index) in heads"
        :key="index"
        :prop="item.field"
        :label="item.name"
        :width="item.width"
      >
        <slot :name="item.field"></slot>
      </el-table-column>
      <slot name="operation"></slot>
    </el-table>
  </div>
</template>

  <script>
export default {
  data() {
    return {};
  },
  props: ["heads", "tableData", "heig"],
  methods: {
    // 查看
    seet(row) {
      console.log(row);
    },
    // 修改
    revise(row) {
      console.log(row);
    },
    // 删除
    deleteRow(row) {
      console.log(row);
    },
    // 表格多选
    handleSelectionChange(val) {
      let multipleSelection = [];
      for (var i = 0; i <= val.length - 1; i++) {
        if (i < val.length - 1) {
          multipleSelection = multipleSelection + val[i].id + ",";
        } else {
          multipleSelection = multipleSelection + val[i].id;
        }
      }
      this.$emit("multipleSelection", multipleSelection);
    },
  },
};
</script>
<style lang="less" scoped>
#record {
  width: 100%;
  height: 100%;
}
</style>