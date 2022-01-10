<template>
  <div id="install">
    <div class="jumpTop">
      <jump :jumpText="jumpText" @cut="cut" />
    </div>
    <div v-if="index === 0"><installOne></installOne></div>
    <div v-else-if="index === 1"><installTwo></installTwo></div>
    <div v-else-if="index === 2"><installThree></installThree></div>
    <div v-else><installFour></installFour></div>
  </div>
</template>

<script>
import jump from "../../../../components/publicS/jump.vue";
import installOne from "../components/installOne.vue";
import installTwo from "../components/installTwo.vue";
import installThree from "../components/installThree.vue";
import installFour from "../components/installFour.vue";
export default {
  data() {
    return {
      jumpText: [
        { name: "商品分类" },
        { name: "商品名称" },
      ],
      index: 0,
    };
  },
  components: {
    jump,
    installOne,
    installTwo,
    installThree,
    installFour,
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
#install {
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