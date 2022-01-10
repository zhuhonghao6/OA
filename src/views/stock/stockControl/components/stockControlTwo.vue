<template>
  <div id="stockControlTwo">
    <!-- 搜索 -->
    <div class="serech2">
      <search></search>
    </div>
    <!-- 按钮 -->
    <div class="stockControlTwo-buttFlex">
      <el-button type="warning" class="butt">导出盘点表</el-button>
    </div>
    <!-- 表格 -->
    <div class="froms">
      <record :heads="heads" :tableData="tableData">
      </record>
    </div>
  </div>
</template>

<script>
import search from "../../../../components/publicS/search.vue";
import record from "../../../../components/publicS/record/record.vue";

export default {
  data() {
    return {
      // 表头
      heads: [
        {
          name: "序号",
          field: "goodsBatch",
        },
        {
          name: "商品名称",
          field: "goodsName",
        },
        {
          name: "规格型号",
          field: "goodsMarque",
        },
        {
          name: "初期数量",
          field: "goodsTrade",
        },
        {
          name: "初期金额（含税）",
          field: "goodsUnit",
          width: "150",
        },
        {
          name: "初期金额（不含税）",
          field: "goodsBatch",
          width: "150",
        },
        {
          name: "本月入库",
          field: "goodsBatch",
        },
        {
          name: "本月出库",
          field: "goodsStockWarning",
        },
        {
          name: "期末数量",
          field: "operation",
        },
        {
          name: "期末金额（含税）",
          field: "operation",
          width: "150",
        },
        {
          name: "期末金额（不含税）",
          field: "operation",
          width: "150",
        },
      ],
      tableData: [],
    };
  },
  components: {
    search,
    record,
  },
};
</script>

<style lang='less'>
#stockControlTwo {
  width: 100%;
  height: 100%;
}
/* <!-- 搜索 --> */
.serech2 {
  position: relative;
  top: 15px;
  width: 60%;
}
// 按钮
.stockControlTwo-buttFlex {
  padding-top: 30px;
  padding-left: 15px;
  .butt {
    height: 32px;
  }
}
// 表格
.froms {
  margin-top: 15px;
}
</style>