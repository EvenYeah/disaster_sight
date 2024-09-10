<template>
  <div class="register-container">
    <el-card class="register-card">
      <h3 class="register-title">用户注册</h3>
      <el-form :model="registerForm" :rules="rules" ref="registerForm" label-width="80px" class="register-form">
        <el-form-item label="用户名" prop="username">
          <el-input v-model="registerForm.username" placeholder="请输入用户名"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="password">
          <el-input type="password" v-model="registerForm.password" placeholder="请输入密码"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="handleRegister">注册</el-button>
          <el-button @click="handleReset">重置</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'Register',
  data() {
    return {
      registerForm: {
        username: '',
        password: ''
      },
      rules: {
        // 只保留必填验证规则
        username: [{ required: true, message: '请输入用户名', trigger: 'blur' }],
        password: [{ required: true, message: '请输入密码', trigger: 'blur' }]
      }
    };
  },
  methods: {
    handleRegister() {
      this.$refs.registerForm.validate((valid) => {
        if (valid) {
          // 在此处调用注册API
          console.log('注册信息：', this.registerForm);
          // 例如，使用 axios 调用 API
          // axios.post('/api/register', this.registerForm).then(response => {
          //   // 注册成功后的处理
          // }).catch(error => {
          //   // 错误处理
          // });
        } else {
          console.log('表单验证失败');
          return false;
        }
      });
    },
    handleReset() {
      this.$refs.registerForm.resetFields();
    }
  }
};
</script>

<style scoped>
.register-container {
  width: 400px;
  margin: 100px auto;
}
.register-card {
  padding: 20px;
}
.register-title {
  text-align: center;
  margin-bottom: 20px;
}
</style>
