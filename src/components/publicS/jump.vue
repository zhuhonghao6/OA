<template>
  <div id="jump">
    <slot>
      <div class="flex">
        <div
          class="jumpIndex"
          v-for="(item, index) in jumpText"
          :key="index"
          @click="ids = index"
          :class="{ white: cut === index }"
        >
          {{ item.name }}
        </div>
      </div>
    </slot>
  </div>
</template>
<script>
export default {
  name: "jump",
  data() {
    return {
      ids: 0,
    };
  },
  props: {
    jumpText: {
      type: Array,
      require: true,
    },
  },
  computed: {
    cut() {
      this.$emit("cut", this.ids*1);
      return this.ids;
    },
  },
};
</script>
<style lang="less">
#jump {
  height: 100%;
  width: 100%;
}
.flex {
  display: flex;
}
.jumpIndex {
  height: 100%;
  padding-left: 30px;
  padding-right: 30px;
  border: 1px;
  font-size: 13px;
}
.white {
  background-color: #fff;
}
</style>