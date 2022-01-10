<template>
  <div id="installTwo">
    <div class="installTwo-buttFlex">
      <el-button type="primary" class="butt">批量添加</el-button>
      <el-button type="primary" class="butt">手动添加</el-button>
      <el-button type="danger" class="butt">批量删除</el-button>
      <el-button type="warning" class="butt">导出报表</el-button>
    </div>
    <!-- 表格 -->
    <div class="installOne-Forms">
      <record :heads="heads" :tableData="tableData">
        <div slot="start">
          <el-table-column type="selection" width="55"> </el-table-column>
        </div>
      </record>
    </div>
  </div>
</template>

<script>
import record from "../../../../components/publicS/record/record.vue";
export default {
  data() {
    return {
      heads: [
        {
          name: "编号",
          field: "id",
        },
        {
          name: "商品名称",
          field: "goodsName",
        },
        {
          name: "所属分类",
          field: "goodsMarque",
        },
        {
          name: "规格型号",
          field: "goodsMarque",
        },
        {
          name: "单位",
          field: "goodsUnit",
        },
        {
          name: "商品备注",
          field: "goodsDownEarlyWarning",
        },
        {
          name: "创建时间",
          field: "goodsDownEarlyWarning",
        },
        {
          name: "操作",
          field: "goodsDownEarlyWarning",
        },
      ],
    };
  },
  components: {
    record,
  },
};
</script>

<style lang='less'>
#installTwo {
  width: 100%;
  height: 100%;
  // 按钮
  .installTwo-buttFlex {
    display: flex;
    width: 35%;
    min-width: 480px;
    padding-top: 20px;
    justify-content: space-around;
    .butt {
      height: 32px;
    }
  }
}
</style>