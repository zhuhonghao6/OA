<template>
  <div id="warehousingOne">
    <div class="warehousingOne-serech">
      <!-- 搜索 -->
      <search> </search>
    </div>
    <!-- 按钮 -->
    <div class="warehousingOne-buttFlex">
      <el-button type="primary" class="butt">批量出库</el-button>
      <el-button type="success" class="butt" @click="warehousManual"
        >手动出库</el-button
      >
      <el-button type="danger" class="butt">批量删除</el-button>
      <el-button type="warning" class="butt">导出报表</el-button>
    </div>
    <!-- 表格 -->
    <div class="warehousingOne-Forms">
      <record :heads="heads" :tableData="tableData" :heig="heig">
        <div slot="start">
          <el-table-column type="selection" width="55"> </el-table-column>
        </div>
      </record>
    </div>
    <!-- 分页 -->
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="page"
      :page-sizes="[10, 20, 30, 40, 50]"
      :page-size="pageSize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="counts"
    >
    </el-pagination>
  </div>
</template>

<script>
import search from "../../../../components/publicS/search.vue";
import record from "../../../../components/publicS/record/record.vue";
import { gets } from "../../../../request/wan";
export default {
  data() {
    return {
      heads: [
        {
          name: "商品名称",
          field: "id",
        },
        {
          name: "批次号",
          field: "goodsName",
        },
        {
          name: "规格型号",
          field: "goodsMarque",
        },
        {
          name: "出库数量",
          field: "goodsTransferNum",
        },
        {
          name: "单位",
          field: "goodsUnit",
        },
        {
          name: "不含税单价",
          field: "callOutSector",
          width: "100",
        },
        {
          name: "不含税金额",
          field: "callInSector",
          width: "100",
        },
        {
          name: "含税单价",
          field: "callOutSector",
        },
        {
          name: "含税金额",
          field: "callInSector",
        },
        {
          name: "税率",
          field: "status",
        },
        {
          name: "税额",
          field: "goodsDownEarlyWarning",
        },
        {
          name: "部门",
          field: "goodsDownEarlyWarning",
        },
        {
          name: "采购类型",
          field: "goodsDownEarlyWarning",
        },
        {
          name: "发票号",
          field: "goodsDownEarlyWarning",
        },
        {
          name: "出库时间",
          field: "goodsDownEarlyWarning",
        },
        {
          name: "操作",
          field: "goodsDownEarlyWarning",
        },
      ],
      page: 1,
      pageSize: 10,
      counts: 50,
      tableData: [],
      heig: "460",
    };
  },
  created() {
    this.paging();
  },
  components: {
    search,
    record,
  },
  methods: {
    // 分页查询
    paging() {
      gets("Goods/getGoodsPage", {
        pagesize: this.pagesize,
        page: this.page,
      }).then((res) => {
        this.counts = res.data.counts;
        this.tableData = res.data.items;
        console.log(res);
      });
    },
    // 每页条数
    handleSizeChange(val) {
      this.pageSize = val;
      this.paging();
    },
    // 页码
    handleCurrentChange(val) {
      this.page = val;
      this.paging();
    },
    // 手动出库
    warehousManual() {
      this.$emit("warehousManual", 1);
    },
  },
};
</script>

<style lang='less'>
#warehousingOne {
  width: 100%;
  height: 100%;
}
/* <!-- 搜索 --> */
.warehousingOne-serech {
  position: relative;
  width: 60%;
}
// 按钮
.warehousingOne-buttFlex {
  display: flex;
  width: 35%;
  min-width: 480px;
  padding-top: 15px;
  justify-content: space-around;
  .butt {
    height: 32px;
  }
}
// 表格
.warehousingOne-Forms {
  margin-top: 15px;
}
</style>