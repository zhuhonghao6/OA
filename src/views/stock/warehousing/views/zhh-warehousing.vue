<template>
  <div id="warehousing">
    <!-- <div class="jumpTop">
      <jump :jumpText="jumpText" @cut="cut" />
    </div> -->
    <div v-if="index === 0">
      <warehousingOne @warehousManual="warehousManual"></warehousingOne>
    </div>
    <div v-else><warehousingTwo></warehousingTwo></div>
  </div>
</template>

<script>
// import jump from "../../../../components/publicS/jump.vue";
import warehousingOne from "../components/warehousingOne.vue";
import warehousingTwo from "../components/warehousingTwo.vue";
export default {
  data() {
    return {
      jumpText: [{ name: "出库记录" }],
      index: 0,
    };
  },
  components: {
    warehousingOne,
    warehousingTwo,
  },
  methods: {
    warehousManual(a) {
      this.index = a * 1;
      console.log(a, 222);
    },
  },
};
</script>

<style>
#warehousing {
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