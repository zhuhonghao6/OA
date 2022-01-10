<template>
  <div id="allocationOne">
    <div class="allocationOne-serech">
      <!-- 搜索 -->
      <search>
        <div slot="denpEnd">
          <el-select v-model="value" placeholder="请选择调入部门">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </div>
      </search>
    </div>
    <!-- 按钮 -->
    <div class="allocationOne-buttFlex">
      <el-button type="danger" class="butt">批量删除</el-button>
      <el-button type="warning" class="butt">导出报表</el-button>
    </div>
    <!-- 表格 -->
    <div class="allocationOne-Forms">
      <record :heads="heads" :tableData="tableData">
        <div slot="start">
          <el-table-column type="selection" width="55"> </el-table-column>
        </div>
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
      options: [],
      value: "",
      heads: [
        {
          name: "调拨编号",
          field: "id",
        },
        {
          name: "产品名称",
          field: "goodsName",
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
          name: "数量",
          field: "goodsTransferNum",
        },
        {
          name: "调出部门",
          field: "callOutSector",
        },
        {
          name: "调入部门",
          field: "callInSector",
        },
        {
          name: "状态",
          field: "status",
        },
        {
          name: "调货时间",
          field: "goodsDownEarlyWarning",
        },
        {
          name: "操作",
          field: "goodsDownEarlyWarning",
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
#allocationOne {
  width: 100%;
  height: 100%;
}
/* <!-- 搜索 --> */
.allocationOne-serech {
  position: relative;
  top: 15px;
  width: 75%;
}
// 按钮
.allocationOne-buttFlex {
  display: flex;
  width: 10%;
  min-width: 230px;
  padding-top: 30px;
  justify-content: space-around;
  .butt {
    height: 32px;
    line-height: 5px;
  }
}
// 表格
.allocationOne-Forms {
  margin-top: 15px;
}
</style>