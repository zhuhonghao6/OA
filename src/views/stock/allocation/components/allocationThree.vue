<template>
  <div id="allocationOne">
    <div class="allocationOne-serech">
      <!-- 搜索 -->
      <search>
        <div slot="denpEnd">
          <el-select v-model="value" placeholder="请选择调入部门">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </div>
      </search>
    </div>
    <div class="allocationOne-buttFlex">
      <el-button type="danger" class="butt">批量删除</el-button>
      <el-button type="warning" class="butt">导出报表</el-button>
    </div>
  </div>
</template>

<script>
import search from "../../../../components/publicS/search.vue";
export default {
  data() {
    return { options: [], value: "" };
  },
  components: {
    search,
  },
};
</script>

<style lang='less'>
#allocationOne {
  width: 100%;
  height: 100%;
}
/* <!-- 搜索 --> */
.allocationOne-serech {
  position: relative;
  top: 15px;
  width: 75%;
}
// 按钮
.allocationOne-buttFlex {
  display: flex;
  width: 10%;
  min-width: 230px;
  padding-top: 30px;
  justify-content: space-around;
  .butt {
    height: 32px;
  }
}
</style>