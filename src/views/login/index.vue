<template>
  <div class="login">
      <el-card class="login-card">
          <div class="logo">
              <img src="../../assets/img/logo_index.png" alt="">
          </div>
        <!-- 表单组件 el-from 表单容器 -->
        <!-- 数据校验 -->
        <el-form ref="loginForm" :model="loginForm" :rules="loginRules" style="margin-top:15px">
            <!-- 表单项 -->
            <el-form-item prop="mobile">
                <!-- 绑定手机号 -->
                <el-input v-model="loginForm.mobile" placeHolder="请输入手机号"></el-input>
            </el-form-item>
            <el-form-item prop="code">
                <!-- 绑定验证码 -->
                <el-input v-model="loginForm.code" placeHolder="请输入验证码" style="width:250px"></el-input>
                <el-button style="float:right">发送验证码</el-button>
            </el-form-item>
            <el-form-item prop="check">
                <!-- 绑定是否勾选协议 -->
                <el-checkbox v-model="loginForm.check" >我已阅读并同意用户协议和隐私条款</el-checkbox>
            </el-form-item>
            <el-form-item>
                <el-button @click="login"  type="primary" style="width:100%" >登录</el-button>
            </el-form-item>
        </el-form>
      </el-card>
  </div>
</template>

<script>
export default {
  data () {
    let validator = function (rule, value, callBack) {
      if (value) {
        callBack()
      } else {
        callBack(new Error('您必须无条件同意被坑'))
      }
    }
    return {
      loginForm: {
        mobile: '', // 手机号
        code: '', // 验证码
        check: false // 是否勾选协议
      },
      // 定义rules 校验规则 表单是根据规则去校验 没有规则 就没有校验
      // key(字段名)：value （数组对象 => 多个=> 一个字段 可能有一个或者多个校验规则 ）
      loginRules: {
        mobile: [
          {
            required: true,
            message: '手机号不能为空'
          },
          {
            pattern: /^1[3456789]\d{9}$/,
            message: '手机格式不正确'
          }
        ],
        code: [
          {
            required: true,
            message: '验证码不能为空'
          },
          {
            pattern: /^\d{6}$/,
            message: '验证码必须为6位数字'
          }
        ],
        check: [
          {
            validator
          }
        ]
      }
    }
  },
  methods: {
    login () {
      // 通过el=form组件的validata方法 校验整个表单的数据
      // 传入一个回调函数 isOk 为true 说明所有的校验规则都成功了
      // 如果为false 说明有错误
      this.$refs.loginForm.validate(isOk => {
        if (isOk) {
          // 请求
          // axios 中 data中放置body参数 params是放置地址参数的
          this.$axios({
            url: '/authorizations',
            method: 'post',
            data: this.loginForm
          })
            .then(result => {
              // 放到前端的缓存中
              window.localStorage.setItem('user-token', result.data.token)
              // 编程式导航
              this.$router.push('/home')
            })
            .catch(() => {
              this.$message({
                message: '手机号或者验证码错误',
                type: 'warning'
              })
            })
        }
      })
    }
  }
}
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
