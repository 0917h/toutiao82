<template>
  <div class="login">
      <el-card class="login-card">
          <div class="logo">
              <img src="../../assets/img/logo_index.png" alt="">
          </div>
        <!-- 表单组件 el-from 表单容器 -->
        <el-form style="margin-top:15px">
            <el-form-item>
                <el-input></el-input>
            </el-form-item>
            <el-form-item>
                <el-input style="width:250px"></el-input>
                <el-button style="float:right">发送验证码</el-button>
            </el-form-item>
            <el-form-item>
                <el-checkbox v-model="checked">我已阅读并同意用户协议和隐私条款</el-checkbox>
            </el-form-item>
            <el-form-item>
                <el-button style="width:100%" type="primary">登录</el-button>
            </el-form-item>
        </el-form>

      </el-card>
  </div>
</template>

<script>
export default {}
</script>

<style lang= 'less' scoped>
.login {
  background: url(../../assets/img/login_bg.jpg);
  height: 100vh;
  display: flex;
  justify-content: center;
  background-size: cover;
  align-items: center;
  .login-card {
    width: 420px;
    height: 330px;
    .logo {
      text-align: center;
      img {
        height: 40px;
      }
    }
  }
}
</style>
