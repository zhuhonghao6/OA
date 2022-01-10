<template>
  <div id="search">
    <slot name="denp" class="distance">
      <el-select v-model="value" placeholder="请选择">
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        >
        </el-option> </el-select
    ></slot>
    <slot name="denpEnd"></slot>
    <slot name="date" class="distance">
      <el-date-picker
        v-model="value2"
        type="daterange"
        :picker-options="pickerOptions"
        range-separator="至"
        start-placeholder="开始日期"
        end-placeholder="结束日期"
        align="right"
      >
      </el-date-picker
    ></slot>
    <slot name="text" class="distance">
      <el-input v-model="value3" placeholder="商品名称"></el-input>
    </slot>
    <el-button type="primary">搜索</el-button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: "",
      value2: "",
      value3: "",
      options:"",
      pickerOptions: {
        shortcuts: [
          {
            text: "最近一周",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit("pick", [start, end]);
            },
          },
          {
            text: "最近一个月",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
              picker.$emit("pick", [start, end]);
            },
          },
          {
            text: "最近三个月",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
              picker.$emit("pick", [start, end]);
            },
          },
        ],
      },
    };
  },
};
</script>

<style>
#search {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: space-between;
}
.el-input {
  width: 200px;
}
</style>