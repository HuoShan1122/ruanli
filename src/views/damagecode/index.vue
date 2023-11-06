<template>
  <div>
  <el-card id="input">
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
      <el-form-item label="灾情码" prop="code">
        <el-input v-model="ruleForm.code" placeholder="code"></el-input>
      </el-form-item>
      <el-form-item label="灾情描述" prop="description">
        <el-input v-model="ruleForm.description" placeholder="description"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
        <el-button @click="resetForm('ruleForm')">重置</el-button>
      </el-form-item>
    </el-form>
  </el-card>

  <el-card>
    <div class="demo-image">
      <div class="block" v-for="fit in fits" :key="fit">
        <span class="demonstration">{{ fit }}</span>
          <el-image
            style="width: 1000px; height: 800px"
            :src="url"
            :fit="fit"></el-image>
      </div>
    </div>
  </el-card>
</div>

</template>

<script>
export default {
  data() {
    return {
      ruleForm: {
        code: "",
        description: ""
      },
      rules: {
        code: [
          { required: true, message: "请输入灾情码", trigger: "blur" }, //失去焦点时触发
          { min: 36, max: 36, message: "长度为36位", trigger: "blur" },
        ],
        description: [
          { required: true, message: "请输入灾情描述", trigger: "blur" },
        ]
      },
      fits: [''],
      url: 'http://1.13.13.22:3341/assets/code.c3eca235.png'
    };
  },
  
  methods: {
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
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
  },
};
</script>

<style>
#input .el-input {
  width: 100%;
  margin-right: 20px;

}
</style>