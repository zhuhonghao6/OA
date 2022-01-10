<template>
  <div id="allocationTwo">
    <div class="allocationTwo-top">
      <!-- 添加表单 -->
      <el-form
        :model="allocationTwoForm"
        :rules="rules"
        ref="allocationTwoForm"
        label-width="100px"
        class="demo-allocationTwoForm"
      >
        <el-col :span="8">
          <el-form-item
            label="调入部门"
            prop="callInSector"
            label-width="140px"
          >
            <el-select
              v-model="allocationTwoForm.callInSector"
              placeholder="请选择活动区域"
            >
              <el-option label="区域一" value="shanghai"></el-option>
              <el-option label="区域二" value="beijing"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
        <el-col :span="8">
          <el-form-item
            label="调出部门"
            prop="callOutSector"
            label-width="140px"
          >
            <el-select
              v-model="allocationTwoForm.callOutSector"
              placeholder="请选择活动区域"
            >
              <el-option label="区域一" value="shanghai"></el-option>
              <el-option
                label="区域二"
                value="beijing"
              ></el-option> </el-select></el-form-item
        ></el-col>
        <el-col :span="7">
          <el-form-item label="操作员" prop="approvalUser" label-width="140px">
            <el-input
              v-model="allocationTwoForm.approvalUser"
            ></el-input> </el-form-item
        ></el-col>
        <el-col :span="8">
          <el-form-item label="产品名称" prop="goodsName" label-width="140px">
            <el-input
              v-model="allocationTwoForm.goodsName"
            ></el-input> </el-form-item
        ></el-col>
        <el-col :span="8">
          <el-form-item
            label="规格型号"
            prop="goodsUpEarlyWarning"
            label-width="140px"
          >
            <el-input
              v-model.number="allocationTwoForm.goodsUpEarlyWarning"
            ></el-input> </el-form-item
        ></el-col>
        <el-col :span="7">
          <el-form-item
            label="申请数量"
            prop="goodsTransferNum"
            label-width="140px"
          >
            <el-input
              v-model.number="allocationTwoForm.goodsTransferNum"
            ></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="23">
          <el-form-item label="备注" prop="remarks" label-width="140px">
            <el-input v-model.number="allocationTwoForm.remarks"></el-input>
          </el-form-item>
        </el-col>
      </el-form>
      <el-button type="success" class="butt" @click="submitForm"
        >添加</el-button
      >
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
    <el-button type="primary" class="buttBott" @click="submitForm"
      >提交</el-button
    >
    <el-button type="primary" class="buttBott" @click="submitForm"
      >重置</el-button
    >
  </div>
</template>

<script>
import record from "../../../../components/publicS/record/record.vue";
import { postp } from "../../../../request/wan";
export default {
  data() {
    return {
      allocationTwoForm: {
        id: "",
        callInSector: "",
        callOutSector: "",
        approvalUser: "",
        goodsName: "",
        goodsUpEarlyWarning: "",
        goodsTransferNum: "",
        remarks: "",
      },
      rules: {
        callInSector: [
          { required: true, message: "请选择调入部门", trigger: "change" },
        ],
        callOutSector: [
          { required: true, message: "请选择调出部门", trigger: "change" },
        ],
        approvalUser: [
          { required: true, message: "请输入操作员", trigger: "change" },
        ],
        goodsName: [
          { required: true, message: "请输入产品名称", trigger: "change" },
        ],
        goodsUpEarlyWarning: [
          { required: true, message: "请输入规格型号", trigger: "change" },
        ],
        goodsTransferNum: [
          { required: true, message: "请输入申请数量", trigger: "change" },
        ],
      },
      heads: [
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
          name: "调入部门",
          field: "goodsUpEarlyWarning",
        },
        {
          name: "调出部门",
          field: "goodsDownEarlyWarning",
        },
        {
          name: "备注",
          field: "goodsDownEarlyWarning",
        },
      ],
      heig: "260",
      page: 1,
      pageSize: 10,
      counts: 50,
      tableData: [],
    };
  },
  components: {
    record,
  },
  methods: {
    // 提交验证
    submitForm() {
      this.$refs["allocationTwoForm"].validate((valid) => {
        if (valid) {
          postp(this.url, this.allocationTwoForm).then((res) => {
            this.$message({
              message: res.data,
              type: "success",
            });
            this.$emit("close", "false");
          });
        } else {
          return false;
        }
      });
    },
    // 重置
    resetForm() {
      this.$refs["allocationTwoForm"].resetFields();
    },
  },
};
</script>

<style lang='less'>
#allocationTwo {
  width: 100%;
  height: 100%;
}
.allocationTwo-top {
  margin-top: 5px;
  display: flex;
  height: 180px;
  background: #fff;
  padding: 10px;
}
.el-form {
  .el-input {
    width: 100%;
  }
  .el-select {
    width: 100%;
  }
}
.butt {
  height: 32px;
  line-height: 5px;
  align-self: flex-end;
  margin-right: 10px;

}
// 表格
.installOne-Forms {
  margin-top: 15px;
}
.buttBott {
  height: 32px;
  line-height: 5px;
  margin-top: 10px;
  margin-right: 10px;
  float: right;
}
</style>