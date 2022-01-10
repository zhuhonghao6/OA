<template>
  <div id="warehousingTwo">
    <div class="warehousingTwoForm">
      <el-form
        :model="installOneAddForm"
        :rules="rules"
        ref="installOneAddForm"
        label-width="100px"
        class="demo-installOneAddForm"
      >
        <el-col :span="12">
          <el-form-item label="所属分类" prop="goodsType" label-width="140px">
            <el-input v-model="installOneAddForm.goodsType"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="商品名称" prop="goodsName" label-width="140px">
            <el-input
              v-model="installOneAddForm.goodsName"
            ></el-input> </el-form-item
        ></el-col>
        <el-col :span="12">
          <el-form-item label="商品型号" prop="goodsMarque" label-width="140px">
            <el-input
              v-model="installOneAddForm.goodsMarque"
            ></el-input> </el-form-item
        ></el-col>
        <el-col :span="12">
          <el-form-item label="所属区县" prop="goodsSector" label-width="140px">
            <el-input
              v-model="installOneAddForm.goodsSector"
            ></el-input> </el-form-item
        ></el-col>
        <el-col :span="12">
          <el-form-item
            label="数量"
            prop="goodsUpEarlyWarning"
            label-width="140px"
          >
            <el-input
              v-model.number="installOneAddForm.goodsUpEarlyWarning"
            ></el-input> </el-form-item
        ></el-col>
        <el-col :span="12">
          <el-form-item
            label="商品下限预警值"
            prop="goodsDownEarlyWarning"
            label-width="140px"
          >
            <el-input
              v-model.number="installOneAddForm.goodsDownEarlyWarning"
            ></el-input>
          </el-form-item>
        </el-col>
      </el-form>
    </div>
  </div>
</template>

<script>
import { postp } from "../../../../request/wan";
export default {
  data() {
    return {
      installOneAddForm: {
        id: "",
        goodsType: "",
        goodsName: "",
        goodsMarque: "",
        goodsSector: "",
        goodsUpEarlyWarning: "",
        goodsDownEarlyWarning: "",
      },
      rules: {
        goodsType: [
          { required: true, message: "请输入类别", trigger: "change" },
        ],
        goodsName: [
          { required: true, message: "请输入名称", trigger: "change" },
        ],
        goodsMarque: [
          { required: true, message: "请输入型号", trigger: "change" },
        ],
        goodsSector: [
          { required: true, message: "请输入单位", trigger: "change" },
        ],
        goodsUpEarlyWarning: [
          { required: true, message: "请输入上限预警", trigger: "change" },
        ],
        goodsDownEarlyWarning: [
          { required: true, message: "请输入下限预警", trigger: "change" },
        ],
      },
    };
  },
  methods: {
    // 提交验证
    submitForm() {
      this.$refs["installOneAddForm"].validate((valid) => {
        if (valid) {
          postp(this.url, this.installOneAddForm).then((res) => {
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
  },
};
</script>

<style lang='less'>
#warehousingTwo {
  width: 100%;
  height: 100%;
}
.warehousingTwoForm {
  width: 90%;
}
.el-form {
  .el-input {
    width: 100%;
  }
  .el-select {
    width: 100%;
  }
}
</style>