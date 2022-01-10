<template>
  <div id="exWarehouseOne">
    <div class="exWarehouseOne-serech">
      <!-- 搜索 -->
      <search> </search>
    </div>
    <div class="exWarehouseOne-buttFlex">
      <el-button type="primary" class="butt" @click="shangchuan = !shangchuan"
        >批量入库</el-button
      >
      <el-button type="success" class="butt" @click="warehousManual"
        >手动入库</el-button
      >
      <!-- <el-button type="danger" class="butt">批量删除</el-button> -->
      <el-button type="warning" class="butt" @click="downloadId"
        >多选导出</el-button
      >
      <el-button type="warning" class="butt" @click="downloadTemp"
        >下载模板</el-button
      >
    </div>
    <!-- 表格 -->
    <div class="exWarehouseOne-Forms">
      <record
        :heads="heads"
        :tableData="tableData"
        :heig="heig"
        @multipleSelection="multipleSelection"
      >
        <div slot="start">
          <el-table-column type="selection" width="55"> </el-table-column>
        </div>
        <div slot="operation">
          <el-table-column label="操作" fixed="right" width="100">
            <template slot-scope="scope">
              <el-button type="text" size="small"
                ><span
                  class="iconfont icon-yanjing xiu a"
                  @click="seet(scope.row)"
                ></span
              ></el-button>
              <!-- <el-button type="text" size="small"
                ><span
                  class="iconfont icon-bianji xiu col"
                  @click="revise(scope.row)"
                ></span
              ></el-button>  -->
              </template
          ></el-table-column>
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
    <!-- 弹出上传 -->
    <!-- 上传 -->
    <el-dialog
      :visible.sync="shangchuan"
      :append-to-body="true"
      title="上传"
      style="width: 800px; margin: auto"
    >
      <div><uploads :uploadUrl="uploadUrl" @success="success"></uploads></div>
      <div slot="footer" class="dialog-footer">
        <el-button @click="shangchuan = false">取 消</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import search from "../../../../components/publicS/search.vue";
import record from "../../../../components/publicS/record/record.vue";
import uploads from "../../../../components/publicS/upload.vue";
import { gets } from "../../../../request/wan";
import URL from "../../../../http/URL2";
export default {
  data() {
    return {
      exWarehouseAddForm: {
        goodsType: "",
        goodsName: "",
        goodsMarque: "",
        goodsSector: "",
        goodsTrade: "",
        goodsNoTaxPrice: "",
        goodsTaxPrice: "",
        goodsTaxRate: "",
        goodsTaxPaid: "",
        goodsPurchaseType: "",
        goodsInvoiceNumbe: "",
        goodsBatch: "",
      },
      heads: [
        {
          name: "商品类别",
          field: "goodsTypeString",
        },
        {
          name: "商品名称",
          field: "goodsName",
        },
        {
          name: "商品型号",
          field: "goodsMarque",
        },
        {
          name: "入库数量",
          field: "goodsTrade",
        },
        {
          name: "单位",
          field: "goodsUnit",
        },
        {
          name: "不含税单价",
          field: "goodsNoTaxPrice",
          width: "100",
        },
        {
          name: "不含税金额",
          field: "goodsNoTaxAmount",
          width: "100",
        },
        {
          name: "含税单价",
          field: "goodsTaxPrice",
        },
        {
          name: "含税金额",
          field: "goodsTaxAmount",
        },
        {
          name: "税率",
          field: "goodsTaxRate",
        },
        {
          name: "税额",
          field: "goodsTaxPaid",
        },
        {
          name: "部门",
          field: "sector",
        },
        {
          name: "采购类型",
          field: "goodsPurchaseType",
        },
        {
          name: "发票号",
          field: "goodsInvoiceNumber",
        },
        {
          name: "批次号",
          field: "goodsBatch",
        },
        {
          name: "最近一次出库时间",
          field: "goodsGoOutTime",
        },
      ],
      page: 1,
      pageSize: 10,
      counts: 50,
      tableData: [],
      heig: "460",
      // 表格导入
      shangchuan: false,
      ids: [],
      uploadUrl: URL.xia + "Goods/insertGoodsByFile",
    };
  },
  created() {
    this.paging();
  },
  components: {
    search,
    record,
    uploads,
  },
  methods: {
    // 分页查询
    paging() {
      // goods、getGoodsPage
      gets("Goods/getGoodsPage", {
        pagesize: this.pageSize,
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
      const data = {
        modify: this.exWarehouseAddForm,
        index: 1,
      };
      const state = {
        news: true,
        seet: false,
        revise: false,
      };
      this.$emit("state", state);
      this.$emit("warehousManual", data);
    },
    // 查看
    seet(res) {
      const state = {
        news: false,
        seet: true,
        revise: false,
        oldData: res,
      };
      this.$emit("state", state);
    },
    // 修改
    revise(res) {
      const state = {
        news: false,
        seet: false,
        revise: true,
        oldData: res,
      };
      this.$emit("state", state);
    },
    // 下载模板
    downloadTemp() {
      window.open(URL.xia + "Goods/goodsDown");
    },
    // 批量上传
    success() {
      this.paging();
      this.shangchuan = !this.shangchuan;
    },
    // 多选ID
    multipleSelection(res) {
      this.ids = res;
    },
    // 多选下载
    downloadId() {
      const ids = this.ids;
      if (ids == "") {
        this.$message.error("请选择人员");
      } else {
        window.open(URL.xia + "Goods/goodsDownById" + "?ids=" + ids);
      }
    },
  },
};
</script>

<style lang='less'>
#exWarehouseOne {
  width: 100%;
  height: 100%;
}
/* <!-- 搜索 --> */
.exWarehouseOne-serech {
  position: relative;
  width: 60%;
}
// 按钮
.exWarehouseOne-buttFlex {
  display: flex;
  width: 30%;
  min-width: 460px;
  padding-top: 15px;
  justify-content: space-around;
  .butt {
    height: 32px;
  }
} // 表格
.exWarehouseOne-Forms {
  margin-top: 15px;
}
</style>