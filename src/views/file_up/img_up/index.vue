<template>
  <el-upload
    class="upload-demo"
    drag
    action="https://jsonplaceholder.typicode.com/posts/"
    multiple>
    <i class="el-icon-upload"></i>
    <div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
    <template #tip>
      <div class="el-upload__tip">
        只能上传 jpg/png 文件，且不超过 500kb
      </div>
    </template>
  </el-upload>
</template>

<script>

</script>

<style>
.upload-demo{
  position: absolute;
  top: 30%;
  left: 35%;
}
</style>
