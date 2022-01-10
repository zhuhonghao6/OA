<template>
  <div id="allocation">
    <div class="jumpTop">
      <jump :jumpText="jumpText" @cut="cut" />
    </div>
    <div v-if="index === 0"><allocationOne></allocationOne></div>
    <div v-else-if="index === 1"><allocationTwo></allocationTwo></div>
    <div v-else-if="index === 2"><allocationThree></allocationThree></div>
    <div v-else><allocationFour></allocationFour></div>
  </div>
</template>

<script>
import jump from "../../../../components/publicS/jump.vue";
import allocationOne from "../components/allocationOne.vue";
import allocationTwo from "../components/allocationTwo.vue";
import allocationThree from "../components/allocationThree.vue";
import allocationFour from "../components/allocationFour.vue";
export default {
  data() {
    return {
      jumpText: [
        { name: "调拨记录" },
        { name: "调拨申请" },
        { name: "请购记录" },
        { name: "请购申请" },
        { name: "审批" },
      ],
      index: 0,
    };
  },
  components: {
    jump,
    allocationOne,
    allocationTwo,
    allocationThree,
    allocationFour,
  },
  methods: {
    cut(a) {
      this.index = a * 1;
      // console.log(a, 222);
    },
  },
};
</script>

<style>
#allocation {
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