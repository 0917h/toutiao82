<template>
<!-- 用el-row el-col -->
  <el-row class="layout-header" type="flex" justify="space-between">
      <!-- span是给col的宽度 elementUI将页面分为24份 -->
      <el-col class="left" :span="6">
          <i class="el-icon-s-unfold icon"></i>
          <span>江苏传智播客教育科技股份有限公司</span>
      </el-col>
      <el-col class="right" :span="3">
        <!-- 属性不给 ： 相当于字符串 -->
          <img class="head-img" :src="userInfo.photo ? userInfo.photo : defaultImg"  alt="">
          <el-dropdown trigger="click" @command="handleMenuItem">
        <!-- 匿名插槽 -->
      <span class="el-dropdown-link">
        {{userInfo.name}}<i class="el-icon-arrow-down el-icon--right"></i>
      </span>
      <!-- 具名插槽 -->
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item command='account'>个人信息</el-dropdown-item>
        <el-dropdown-item command='git'>git地址</el-dropdown-item>
        <el-dropdown-item command='lgout '>退出</el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
      </el-col>
  </el-row>
</template>

<script>
export default {
  data () {
    return {
      userInfo: {},
      defaultImg: require('../../assets/img/avatar.jpg')
    }
  },
  methods: {
    // 获取用户数据
    getUserInfo () {
      this.$axios({
        url: '/user/profile'
      }).then(result => {
        this.userInfo = result.data
      })
    },
    // 点击菜单触发的方法
    handleMenuItem (command) {
      if (command === 'account') {
        // 账户信息
      } else if (command === 'git') {
        // git地址
        window.location.href = 'http://github.com/shuiruohanyu/82heimatoutiao'
      } else {
        window.localStorage.clear()
        this.$router.push('/login')
      }
    }
  },
  created () {
    this.getUserInfo()
  }
}
</script>

<style lang='less' scoped>
.layout-header {
  padding: 10px 0;
  .left {
    .icon {
      font-size: 22px;
      margin-right: 3px;
    }
    display: flex;
    align-items: center;
  }
  .right {
    display: flex;
    align-items: center;
  }
  .head-img {
    border-radius: 50px;
    margin-right: 5px;
    width: 40px;
    height: 40px;
  }
}
</style>
