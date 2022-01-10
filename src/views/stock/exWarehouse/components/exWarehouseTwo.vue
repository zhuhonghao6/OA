<template>
  <div id="exWarehouseTwo">
    <div class="exWarehouseTwoForm">
      <el-form
        :model="exWarehouseForm"
        :rules="rules"
        ref="exWarehouseForm"
        :label-width="width"
        class="demo-exWarehouseForm"
      >
        <el-col :span="12">
          <el-form-item label="所属分类" prop="goodsType" :label-width="width">
            <el-select
              v-model="exWarehouseForm.goodsType"
              placeholder="请选择所属分类"
              @change="obtainName"
              :disabled="true"
            >
              <el-option
                v-for="(item, index) in selets.goodsType"
                :key="index"
                :label="item"
                :value="item"
              ></el-option>
            </el-select>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="商品名称" prop="goodsName" :label-width="width">
            <el-select
              v-model="exWarehouseForm.goodsName"
              placeholder="请选择商品名称"
              @change="obtainMarque"
            >
              <el-option
                v-for="(item, index) in selets.goodsName"
                :key="index"
                :label="item"
                :value="item"
              ></el-option> </el-select></el-form-item
        ></el-col>
        <el-col :span="12">
          <el-form-item
            label="商品型号"
            prop="goodsMarque"
            :label-width="width"
          >
            <el-select
              v-model="exWarehouseForm.goodsMarque"
              placeholder="请选择商品型号"
            >
              <el-option
                v-for="(item, index) in selets.goodsMarque"
                :key="index"
                :label="item.goodsMarque"
                :value="item.goodsMarque"
              ></el-option> </el-select></el-form-item
        ></el-col>
        <el-col :span="12">
          <el-form-item
            label="所属区县"
            prop="goodsSector"
            :label-width="width"
          >
            <el-select
              v-model="exWarehouseForm.goodsSector"
              placeholder="请选择所属区县"
            >
              <el-option
                v-for="(department, index) in department"
                :key="index"
                :label="department.label"
                :value="department.id"
              ></el-option>
            </el-select> </el-form-item
        ></el-col>
        <el-col :span="12">
          <el-form-item label="数量" prop="goodsTrade" :label-width="width">
            <el-input
              v-model.number="exWarehouseForm.goodsTrade"
            ></el-input> </el-form-item
        ></el-col>
        <el-col :span="12">
          <el-form-item
            label="不含税单价"
            prop="goodsNoTaxPrice"
            :label-width="width"
          >
            <el-input
              v-model.number="exWarehouseForm.goodsNoTaxPrice"
            ></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item
            label="含税单价"
            prop="goodsTaxPrice"
            :label-width="width"
          >
            <el-input v-model.number="exWarehouseForm.goodsTaxPrice"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="税率" prop="goodsTaxRate" :label-width="width">
            <el-input v-model="exWarehouseForm.goodsTaxRate"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item
            label="商品单个税额"
            prop="goodsTaxPaid"
            :label-width="width"
          >
            <el-input v-model.number="exWarehouseForm.goodsTaxPaid"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item
            label="采购类型"
            prop="goodsPurchaseType"
            :label-width="width"
          >
            <el-input v-model="exWarehouseForm.goodsPurchaseType"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item
            label="发票号"
            prop="goodsInvoiceNumber"
            :label-width="width"
          >
            <el-input v-model="exWarehouseForm.goodsInvoiceNumber"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="批次号" prop="goodsBatch" :label-width="width">
            <el-input v-model="exWarehouseForm.goodsBatch"></el-input>
          </el-form-item>
        </el-col>
      </el-form>
    </div>
    <!-- 按钮 -->
    <div class="exWarehouseTwo-buttFlex">
      <el-button type="primary" class="butt" @click="submitForm"
        >提交</el-button
      >
      <el-button type="primary" class="butt" @click="upper">返回</el-button>
    </div>
  </div>
</template>

<script>
import { postp, gets } from "../../../../request/wan";
export default {
  data() {
    return {
      exWarehouseForm: {
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
        goodsInvoiceNumber: "",
        goodsBatch: "",
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
        goodsTrade: [
          { required: true, message: "请输入数量", trigger: "change" },
        ],
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
          { required: true, message: "请输入商品单个税率", trigger: "change" },
        ],
        goodsPurchaseType: [
          { required: true, message: "请输入采购类型", trigger: "change" },
        ],
        goodsInvoiceNumber: [
          { required: true, message: "请输入发票号", trigger: "change" },
        ],
        goodsBatch: [
          { required: true, message: "请输入批次号", trigger: "change" },
        ],
      },
      width: "110px",
      // 下拉框选项
      selets: {
        goodsType: [],
        goodsName: [],
        goodsMarque: [],
      },
      data: [],
      department: [],
      url: "Goods/insertGoods",
    };
  },
  created() {
    this.initialData("goodsType");
    this.three();
    this.reads();
    console.log(this.stateData);
  },
  methods: {
    // 读取数据
    reads() {
      this.exWarehouseForm = this.parameter;
      // console.log(this.parameter, "读取");
    },
    // 获取分类
    initialData(i) {
      gets("GoodsTypes/getGoodsTypesType", {
        type: this.exWarehouseForm.goodsType,
        name: this.exWarehouseForm.goodsName,
      }).then((res) => {
        this.selets[i] = res.data;
      });
    },
    // 组织构架
    three() {
      // 组织构架
      gets("sector/getSector").then((res) => {
        this.data = res.data;
        this.qing();
        // console.log("d ",this.data)
      });
    },
    // 自动获取部门
    qing() {
      var aa = 0;
      Object.keys(this.data[0]).forEach((key) => {
        if (key == "children") {
          aa = 1;
        }
      });
      if (aa == 1) {
        for (var i = 0; i < this.data[0].children.length; i++) {
          const a = this.data[0].children[i].UpSector;
          if (a != 0 && a != 26) {
            this.department.push(this.data[0].children[i]);
          }
          for (var j = 0; j < this.data[0].children[i].children.length; j++) {
            const a = this.data[0].children[i].children[j].UpSector;
            if (a != 0 && a != 26) {
              this.department.push(this.data[0].children[i].children[j]);
            }
          }
        }
      } else {
        const a = this.data[0].UpSector;
        if (a != 0 && a != 26) {
          this.department.push(this.data[0]);
        }
      }
    },
    // 获取商品
    obtainName() {
      this.selets.goodsName = [];
      this.exWarehouseForm.goodsName = "";
      this.exWarehouseForm.goodsMarque = "";
      this.initialData("goodsName");
    },
    // 获取型号
    obtainMarque() {
      this.selets.goodsMarque = [];
      this.exWarehouseForm.goodsMarque = "";
      this.initialData("goodsMarque");
    },
    // 寻找分类id
    findId(data, name) {
      data.forEach((res) => {
        if (res.goodsMarque == name) {
          this.exWarehouseForm["goodsType"] = res.id;
        }
      });
    },
    // 寻找部门id
    findSector(name) {
      this.department.forEach((res) => {
        if ((res.label = name)) {
          this.exWarehouseForm["goodsSector"] = res.id;
        }
      });
    },
    // 提交验证
    submitForm() {
      this.$refs["exWarehouseForm"].validate((valid) => {
        if (valid) {
          this.findId(
            this.selets.goodsMarque,
            this.exWarehouseForm.goodsMarque
          );
          this.findSector(this.exWarehouseForm.goodsSector);
          postp(this.url, this.exWarehouseForm).then((res) => {
            this.$message({
              message: res.data,
              type: "success",
            });
            const data = { index: 0 };
            this.$emit("upper", data);
            this.$emit("close", "false");
          });
        } else {
          return false;
        }
      });
    },
    // 返回
    upper() {
      const data = {
        parameter: this.exWarehouseForm,
        index: 0,
      };
      this.$emit("upper", data);
    },
  },
  props: ["parameter", "stateData"],
};
</script>

<style lang='less'>
#exWarehouseTwo {
  width: 100%;
  height: 100%;
}
.exWarehouseTwoForm {
  width: 100%;
  height: 400px;
  background-color: #fff;
  padding-top: 20px;
  .el-form {
    .el-input {
      width: 80%;
    }
    .el-select {
      width: 100%;
    }
  }
}

.exWarehouseTwo-buttFlex {
  width: 100%;

  .butt {
    height: 32px;
    line-height: 5px;
    margin: 20px 0px 20px 20px;
  }
}
</style>