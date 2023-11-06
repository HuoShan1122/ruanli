<template>
  <div>
    <el-card>
      <el-form ref="form" :model="form" label-width="80px">
        <el-form-item label="上传文件">
          <el-upload
            class="upload-demo"
            drag
            action="https://jsonplaceholder.typicode.com/posts/"
            multiple
          >
            <i class="el-icon-upload"></i>
            <div class="el-upload__text">
              将文件拖到此处，或<em>点击上传</em>
            </div>
            <div class="el-upload__tip" slot="tip">
              只能上传jpg/png文件，且不超过500kb
            </div>
          </el-upload>
        </el-form-item>

        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm')"
            >提交</el-button
          >
        </el-form-item>
      </el-form>
    </el-card>

    <el-card>
      <h2>说明</h2>
      <p>仅有一个文件时请将文件名写为灾情码。某灾情码有多个文件时，请将多个文件中的一个文件名改为灾情码。</p>
      <p>切勿将多个文件名改为同一个灾情码。同样，禁止多个文件名中存在多个灾情码。</p>
      <p>这些操作都会导致灾情信息上传的失败。</p>
    </el-card>
  </div>
</template>
  
  <script>
export default {
  methods: {
    handleChange(value) {
      console.log(value);
    },
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
  },
};
</script>
  
  <style>
</style>