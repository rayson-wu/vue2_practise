<template>
  <div class="container">
    <!-- 背景图 -->
    <div class="bg"></div>
    <!-- 登录框 -->
    <div class="login">
      <h1>登录</h1>
      <el-form :model="loginForm" :rules="rules" ref="ruleForm" hide-required-asterisk="true" status-icon="true">
        <el-form-item label='用户名' prop="username">
          <el-input v-model="loginForm.username" prefix-icon="el-icon-user-solid" />
        </el-form-item>
        <el-form-item label='密码' prop="password">
          <el-input type="password"
          v-model="loginForm.password"
          prefix-icon="el-icon-lock"
          auto-complete="off">
          </el-input>
        </el-form-item>
        <el-button type="primary" class="btn" @click="login">登录</el-button>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loginForm: {
        username: '',
        password: ''
      },
      rules: {
        username: [{ required: true, message: '用户名不能为空', trigger: 'blur' }],
        password: [
          { required: true, message: '密码不能为空', trigger: 'blur' },
          { min: 6, message: '密码不能少于6位', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    login () {
      this.$refs.ruleForm.validate(valid => {
        if (!valid) {
          return false
        } else {
          this.$refs.ruleForm.resetFields()
          // TODO 调用接口登录
          this.$router.replace('/')
        }
      })
    }
  }
}
</script>

<style lang='scss' scoped>
.container {
  position: relative;
  width: 100vw;
  height: 100vh;
  .bg {
    width: 100%;
    height: 100%;
    background-image: url('@/assets/bg.jpg');
    background-size: cover;
    background-position: center;
  }
  .login {
    position: absolute;
    left: 500px;
    top: 200px;
    width: 500px;
    height: 300px;
    background-color: rgba(255,255,255,.8);
    border-radius: 10px;
    padding: 10px 20px;
    .btn {
      width: 100%;
    }
    .see-pw {
      cursor: pointer;
    }
  }
}
</style>
