<template>
  <div id="stockControlOneModify">
    <el-form
      :model="stockControlOneModifyForm"
      :rules="rules"
      ref="stockControlOneModifyForm"
      label-width="100px"
      class="demo-stockControlOneModifyForm"
    >
      <el-col :span="12">
        <el-form-item label="商品类别" label-width="140px">
          <el-input
            v-model.number="stockControlOneModifyForm.goodsTypeString"
          ></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="12">
        <el-form-item label="商品名称" label-width="140px">
          <el-input
            v-model.number="stockControlOneModifyForm.goodsName"
          ></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="12">
        <el-form-item label="商品型号" label-width="140px">
          <el-input
            v-model.number="stockControlOneModifyForm.goodsMarque"
          ></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="12">
        <el-form-item label="入库数量" label-width="140px">
          <el-input
            v-model.number="stockControlOneModifyForm.goodsTrade"
          ></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="12">
        <el-form-item label="单位" label-width="140px">
          <el-input
            v-model.number="stockControlOneModifyForm.goodsUnit"
          ></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="12">
        <el-form-item label="部门" label-width="140px">
          <el-input
            v-model.number="stockControlOneModifyForm.sector"
          ></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="12">
        <el-form-item label="批次号" label-width="140px">
          <el-input
            v-model.number="stockControlOneModifyForm.goodsBatch"
          ></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="12">
        <el-form-item
          label="不含税单价"
          prop="goodsNoTaxPrice"
          label-width="140px"
        >
          <el-input
            v-model="stockControlOneModifyForm.goodsNoTaxPrice"
          ></el-input> </el-form-item
      ></el-col>
      <el-col :span="12">
        <el-form-item label="含税单价" prop="goodsTaxPrice" label-width="140px">
          <el-input
            v-model="stockControlOneModifyForm.goodsTaxPrice"
          ></el-input> </el-form-item
      ></el-col>
      <el-col :span="12">
        <el-form-item label="税率" prop="goodsTaxRate" label-width="140px">
          <el-input
            v-model="stockControlOneModifyForm.goodsTaxRate"
          ></el-input> </el-form-item
      ></el-col>
      <el-col :span="12">
        <el-form-item
          label="商品单个税额"
          prop="goodsTaxPaid"
          label-width="140px"
        >
          <el-input
            v-model.number="stockControlOneModifyForm.goodsTaxPaid"
          ></el-input> </el-form-item
      ></el-col>
      <el-col :span="12">
        <el-form-item
          label="采购类型"
          prop="goodsPurchaseType"
          label-width="140px"
        >
          <el-input
            v-model.number="stockControlOneModifyForm.goodsPurchaseType"
          ></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="12">
        <el-form-item
          label="发票号"
          prop="goodsInvoiceNumber"
          label-width="140px"
        >
          <el-input
            v-model.number="stockControlOneModifyForm.goodsInvoiceNumber"
          ></el-input>
        </el-form-item>
      </el-col>
    </el-form>
  </div>
</template>

<script>
import { postp } from "../../../../request/wan";
export default {
  data() {
    return {
      stockControlOneModifyForm: {
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
      rules: {
        goodsNoTaxPrice: [
          { required: true, message: "请输入不含税单价", trigger: "change" },
        ],
        goodsTaxPrice: [
          { required: true, message: "请输入含税单价", trigger: "change" },
        ],
        goodsTaxRate: [
          { required: true, message: "请输入税率", trigger: "change" },
        ],
        goodsTaxPaid: [
          { required: true, message: "请输入商品单个税额", trigger: "change" },
        ],
        goodsPurchaseType: [
          { required: true, message: "请输入采购类型", trigger: "change" },
        ],
        goodsInvoiceNumber: [
          { required: true, message: "请输入发票号", trigger: "change" },
        ],
      },
      url: "",
    };
  },
  created() {
    this.judge();
  },
  props: ["state", "stockControlData"],

  methods: {
    // 判断
    judge() {
      this.stockControlOneModifyForm = this.stockControlData;
      if (this.state.news) {
        this.url = "GoodsTypes/insertGoodsTypes";
      } else {
        this.url = "GoodsTypes/updateGoodsType";
      }
    },
    // 提交验证
    submitForm() {
      this.$refs["stockControlOneModifyForm"].validate((valid) => {
        if (valid) {
          postp("123", this.stockControlOneModifyForm).then((res) => {
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
      this.$refs["stockControlOneModifyForm"].resetFields();
    },
  },
  watch: {
    state() {
      this.judge();
    },
  },
};
</script>

<style lang='less'>
#stockControlOneModify {
  width: 100%;
  height: 100%;
}
.el-form {
  .el-input {
    width: 100%;
  }
}
</style>