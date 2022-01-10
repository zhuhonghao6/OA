<template>
  <div class="upload">
    <!-- 上传 -->
    <el-upload
      class="upload-demo"
      drag
      :action="uploadUrl"
      multiple
      :headers="myHeaders"
      :on-success="ok"
      :on-error="no"
    >
      <i class="el-icon-upload"></i>
      <div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
      <div class="el-upload__tip" slot="tip"></div>
    </el-upload>
  </div>
</template>

<script>
var token = sessionStorage.getItem("token");
export default {
  data() {
    return {
      // 导入文件
      myHeaders: { token: token },
    };
  },
  methods: {
    // 导入成功
    ok(response) {
      this.$emit("success");
      this.$confirm(response, "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      }).then(() => {});
    },
    //  导入失败
    no(res) {
      this.$confirm(res, "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      }).then(() => {});
    },
  },
  props: ["uploadUrl"],
};
</script>

<style>
.upload {
  width: 100%;
  height: 100%;
}
</style>