<template>
  <div id="stockControlOne">
    <div class="serech1">
      <!-- 搜索 -->
      <search>
        <div slot="date">
          <el-col :span="11">
            <el-select v-model="value" placeholder="库存量">
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              >
              </el-option> </el-select
          ></el-col>
          <el-col :span="11" :offset="2">
            <el-select v-model="value" placeholder="选择批次">
              <el-option
                v-for="item in options2"
                :key="item.value2"
                :label="item.label"
                :value="item.value"
              >
              </el-option> </el-select
          ></el-col>
        </div>
      </search>
    </div>
    <!-- 按钮 -->
    <div class="stockControlOne-buttFlex">
      <el-button type="primary" class="butt">批量修改</el-button>
      <el-button type="warning" class="butt">导出报表</el-button>
    </div>
    <!-- 表格 -->
    <div class="stockControlOne-froms">
      <record :heads="heads" :tableData="tableData" :heig="heig">
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
              <el-button type="text" size="small"
                ><span
                  class="iconfont icon-bianji xiu col"
                  @click="revise(scope.row)"
                ></span
              ></el-button> </template
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
    <!-- 修改 -->
    <el-dialog
      title="提示"
      :visible.sync="stockControlOneModify"
      :append-to-body="true"
      width="50%"
      :before-close="handleClose"
    >
      <stockControlOneModify
        :stockControlData="stockControlData"
        :state="state"
        ref="stockControlOneModify"
        @close="close"
        v-if="sign"
      ></stockControlOneModify>
      <span slot="footer" class="dialog-footer">
        <el-button @click="stockControlOneModify = false">取 消</el-button>
        <el-button v-if="!state.seet" @click="stockControlOneModifyRef"
          >重置</el-button
        >
        <el-button
          v-if="!state.seet"
          type="primary"
          @click="stockControlOneSubmit"
          >确 定</el-button
        >
      </span>
    </el-dialog>
  </div>
</template>

<script>
import search from "../../../../components/publicS/search.vue";
import record from "../../../../components/publicS/record/record.vue";
import stockControlOneModify from "./stockControlOneModify.vue";
import { gets } from "../../../../request/wan";
export default {
  data() {
    return {
      value: "",
      value2: "",
      options: [],
      options2: [],
      // 表头
      heads: [
        {
          name: "批次号",
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
          name: "数量",
          field: "goodsTrade",
        },
        {
          name: "单位",
          field: "goodsUnit",
        },
        {
          name: "所属分类",
          field: "goodsTypeString",
        },
        {
          name: "部门",
          field: "sector",
        },
        {
          name: "预警",
          field: "goodsStockWarning",
        },
      ],
      page: 1,
      pageSize: 10,
      counts: 50,
      tableData: [],
      heig: "410",
      stockControlOneModify: false,
      // 状态
      state: {
        seet: false,
        revise: false,
      },
      // 单条数据
      stockControlDataData: {
        goodsTypeString: "",
        goodsName: "",
        goodsMarque: "",
        goodsTrade: "",
        goodsUnit: "",
        sector: "",
        goodsBatch: "",
        goodsNoTaxPrice: "",
        goodsTaxPrice: "",
        goodsTaxRate: "",
        goodsTaxPaid: "",
        goodsPurchaseType: "",
        goodsInvoiceNumber: "",
      },
    };
  },
  computed: {
    sign() {
      if (this.state.seet || this.state.revise) {
        console.log(1);
        return true;
      } else {
        console.log(2);
        return false;
      }
    },
  },
  components: {
    search,
    record,
    stockControlOneModify,
  },
  created() {
    this.paging();
  },
  methods: {
    // 状态刷新
    newState() {
      this.state = {
        seet: false,
        revise: false,
      };
      this.stockControlData = {
        goodsType: "",
        goodsName: "",
        goodsMarque: "",
        goodsUnit: "",
        goodsUpEarlyWarning: "",
        goodsDownEarlyWarning: "",
      };
      this.stockControlOneModify = false;
      this.paging();
    },
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
    // 重置
    stockControlOneModifyRef() {
      this.$refs.stockControlOneModify.resetForm();
    },
    // 提交
    stockControlOneSubmit() {
      this.$refs.stockControlOneModify.submitForm();
    },
    // 关闭提示
    handleClose(done) {
      this.$confirm("确认关闭？")
        .then(() => {
          done();
          this.newState();
        })
        .catch(() => {});
    },
    // 成功后的回调
    close() {
      // this.paging();
      this.newState();
    },
    // 查看
    seet(res) {
      this.stockControlOneModify = !this.stockControlOneModify;
      this.state.seet = true;
      this.stockControlData = res;
    },
    // 修改
    revise(res) {
      this.stockControlOneModify = !this.stockControlOneModify;
      this.state.revise = true;
      this.stockControlData = res;
      console.log(res);
    },
  },
  watch: {
    stockControlOneModify() {
      if (!this.stockControlOneModify) {
        this.newState();
      }
    },
  },
};
</script>

<style lang='less'>
#stockControlOne {
  width: 100%;
  height: 100%;
}
/* <!-- 搜索 --> */
.serech1 {
  position: relative;
  top: 15px;
  width: 68%;
}
// 按钮
.stockControlOne-buttFlex {
  display: flex;
  width: 10%;
  min-width: 230px;
  padding-top: 30px;
  justify-content: space-around;
  .butt {
    height: 32px;
  }
}
// 表格
.stockControlOne-froms {
  margin-top: 15px;
}
</style>