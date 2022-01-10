<template>
  <div id="exWarehouse">
    <!-- <div class="jumpTop">
      <jump :jumpText="jumpText" @cut="cut" />
    </div> -->
    <div v-if="index === 0">
      <exWarehouseOne @warehousManual="cut" @state="state"></exWarehouseOne>
    </div>
    <div v-else>
      <exWarehouseTwo
        @upper="cut"
        :parameter="parameter"
        :stateData="stateData"
      ></exWarehouseTwo>
    </div>
  </div>
</template>

<script>
// import jump from "../../../../components/publicS/jump.vue";
import exWarehouseOne from "../components/exWarehouseOne.vue";
import exWarehouseTwo from "../components/exWarehouseTwo.vue";
export default {
  data() {
    return {
      jumpText: [{ name: "入库记录" }, { name: "手动入库" }],
      index: 0,
      parameter: {
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
      stateData: {},
    };
  },
  components: {
    exWarehouseOne,
    exWarehouseTwo,
  },
  methods: {
    // 页面判断
    cut(res) {
      this.index = res.index * 1;
      res.parameter ? (this.parameter = res.parameter) : true;
    },
    // 状态
    state(res) {
      this.index = res.index * 1;
      this.stateData = res;
    },
  },
};
</script>

<style>
#exWarehouse {
  width: 100%;
  height: 100%;
}
.jumpTop {
  width: 100%;
  height: 40px;
  line-height: 40px;
  background-color: #cccccc;
}
</style>