<template>
  <div id="installThree">
    <div class="installThree-buttFlex">
      <el-button type="primary" class="butt">批量添加</el-button>
      <el-button type="primary" class="butt">手动添加</el-button>
      <el-button type="danger" class="butt">批量删除</el-button>
      <el-button type="warning" class="butt">导出报表</el-button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return { options: [], value: "" };
  },
};
</script>

<style lang='less'>
#installThree {
  width: 100%;
  height: 100%;
  // 按钮
  .installThree-buttFlex {
    display: flex;
    width: 35%;
    min-width: 480px;
    padding-top: 20px;
    justify-content: space-around;
    .butt {
      height: 32px;
    }
  }
}
</style>