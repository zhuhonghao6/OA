<template>
  <div id="stockControl">
    <div class="jumpTop">
      <jump :jumpText="jumpText" @cut="cut" />
    </div>
    <div v-if="index === 0"><stockControlOne></stockControlOne></div>
    <div v-else><stockControlTwo></stockControlTwo></div>
  </div>
</template>

<script>
import jump from "../../../../components/publicS/jump.vue";
import stockControlOne from "../components/stockControlOne.vue";
import stockControlTwo from "../components/stockControlTwo.vue";
export default {
  data() {
    return {
      jumpText: [{ name: "库存列表" }, { name: "盘点表" }],
      index: 0,
    };
  },
  components: { jump, stockControlOne, stockControlTwo },
  methods: {
    cut(a) {
      this.index = a * 1;
      // console.log(a, 222);
    },
  },
};
</script>

<style>
#stockControl {
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