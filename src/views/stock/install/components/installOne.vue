<template>
  <div id="installOne">
    <!-- 按钮 -->
    <div class="installOne-buttFlex">
      <el-button type="primary" class="butt">批量添加</el-button>
      <el-button type="primary" class="butt" @click="add">手动添加</el-button>
      <el-button type="danger" class="butt">批量删除</el-button>
      <el-button type="warning" class="butt">导出报表</el-button>
    </div>
    <!-- 表格 -->
    <div class="installOne-Forms">
      <record :heads="heads" :tableData="tableData" :heig="heig">
        <div slot="start">
          <el-table-column type="selection" width="55"> </el-table-column>
        </div>
        <div slot="operation">
          <el-table-column label="操作" fixed="right">
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
    <!-- 分类添加 -->
    <el-dialog
      title="提示"
      :visible.sync="installOneAdd"
      :append-to-body="true"
      width="50%"
      :before-close="handleClose"
    >
      <installOneAdd
        :installData="installData"
        :state="state"
        ref="installOneAdd"
        @close="close"
        v-if="sign"
      ></installOneAdd>
      <span slot="footer" class="dialog-footer">
        <el-button @click="installOneAdd = false">取 消</el-button>
        <el-button v-if="!state.seet" @click="installOneAddRef">重置</el-button>
        <el-button v-if="!state.seet" type="primary" @click="installOneSubmit"
          >确 定</el-button
        >
      </span>
    </el-dialog>
  </div>
</template>

<script>
import record from "../../../../components/publicS/record/record.vue";
import installOneAdd from "./installOneAdd.vue";
import { gets } from "../../../../request/wan";
export default {
  data() {
    return {
      heads: [
        {
          name: "编号",
          field: "id",
        },
        {
          name: "商品类别",
          field: "goodsType",
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
          name: "商品单位",
          field: "goodsUnit",
        },
        {
          name: "商品上限预警值",
          field: "goodsUpEarlyWarning",
        },
        {
          name: "商品下限预警值",
          field: "goodsDownEarlyWarning",
        },
      ],
      heig: "460",
      page: 1,
      pageSize: 10,
      counts: 50,
      tableData: [],
      installOneAdd: false,
      // 状态
      state: {
        news: false,
        seet: false,
        revise: false,
      },
      // 单条数据
      installData: {
        id: "",
        goodsType: "",
        goodsName: "",
        goodsMarque: "",
        goodsUnit: "",
        goodsUpEarlyWarning: "",
        goodsDownEarlyWarning: "",
      },
    };
  },
  created() {
    this.paging();
  },
  computed: {
    sign() {
      if (this.state.seet || this.state.news || this.state.revise) {
        console.log(1);
        return true;
      } else {
        console.log(2);
        return false;
      }
    },
  },
  components: {
    record,
    installOneAdd,
  },
  methods: {
    // 状态刷新
    newState() {
      this.state = {
        news: false,
        seet: false,
        revise: false,
      };
      this.installData = {
        id: "",
        goodsType: "",
        goodsName: "",
        goodsMarque: "",
        goodsUnit: "",
        goodsUpEarlyWarning: "",
        goodsDownEarlyWarning: "",
      };
      this.installOneAdd = false;
      this.paging();
    },
    // 分页查询
    paging() {
      gets("GoodsTypes/getGoodsTypesPage", {
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
    // 新增
    add() {
      this.installOneAdd = !this.installOneAdd;
      this.state.news = true;
      this.$refs.installOneAdd?.resetForm();
    },
    // 重置
    installOneAddRef() {
      this.$refs.installOneAdd.resetForm();
    },
    // 提交
    installOneSubmit() {
      this.$refs.installOneAdd.submitForm();
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
      this.installOneAdd = !this.installOneAdd;
      this.state.seet = true;
      this.installData = res;
    },
    // 修改
    revise(res) {
      this.installOneAdd = !this.installOneAdd;
      this.state.revise = true;
      this.installData = res;
      console.log(res);
    },
  },
  watch: {
    installOneAdd() {
      if (!this.installOneAdd) {
        this.newState();
      }
    },
  },
};
</script>

<style lang='less'>
#installOne {
  width: 100%;
  height: 100%;
  // 按钮
  .installOne-buttFlex {
    display: flex;
    width: 35%;
    min-width: 480px;
    padding-top: 20px;
    justify-content: space-around;
    .butt {
      height: 32px;
      line-height: 5px;
    }
  }
}
// 表格
.installOne-Forms {
  margin-top: 15px;
}
</style>