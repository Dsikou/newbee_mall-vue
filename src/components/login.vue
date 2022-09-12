<template>
  <div id="login_Background">
    <div class="login_logo">vei ni bruin</div>
    <div class="login_card">
      <el-card class="box-card">
        <div class="login_form">
          <el-input v-model="userName" placeholder="请输入内容"></el-input>
          <el-input placeholder="请输入密码" v-model="passWord" show-password></el-input>
          <el-button type="primary">登录</el-button>
        </div>
      </el-card>
    </div>
    <div class="login_clock">
      <div class="time">{{time}}</div>
      <div class="date">{{date}}</div>
    </div>
    <div class="login_copyright">Copyright © 2022 vei ni bruin All Rights Reserved.</div>
  </div>
</template>

<script>

export default {
  name: 'login',
  data () {
    return {
      userName: '',
      passWord: '',
      time: '',
      date: ''
    }
  },
  mounted () {
    this.$nextTick(() => {
      setInterval(this.update_clock, 1000)
    })
  },
  methods: {
    update_clock: function (e) {
      var d = new Date()
      var year = d.getFullYear()
      if (year < 10) {
        year = '0' + year
      }
      var month = d.getMonth()
      if (month < 10) {
        month = '0' + month
      }
      var day = d.getDate()
      if (day < 10) {
        day = '0' + day
      }
      var hours = d.getHours()
      if (hours < 10) {
        hours = '0' + hours
      }
      var minutes = d.getMinutes()
      if (minutes < 10) {
        minutes = '0' + minutes
      }
      var secodes = d.getSeconds()
      if (secodes < 10) {
        secodes = '0' + secodes
      }
      this.time = hours + ':' + minutes + ':' + secodes
      this.date = year + '/' + month + '/' + day
    }
  }
}
</script>
<!--scoped 只在此组件生效-->
<style scoped>
@import url('../assets/css/login/loginStyle.css');
</style>
