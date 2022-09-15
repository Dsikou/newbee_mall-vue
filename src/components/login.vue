<template>
  <div id="login_Background">
    <div class="login_logo">Oboro month era</div>
    <div class="login_card">
      <el-card class="box-card">
        <div class="login_form">
          <el-input v-model="userName" placeholder="请输入账户"></el-input>
          <el-input placeholder="请输入密码" v-model="passWord" show-password></el-input>
          <el-button type="primary" v-on:click="login_up">登录</el-button>
        </div>
      </el-card>
    </div>
    <div class="login_clock">
      <div class="time">{{time}}</div>
      <div class="date">{{date}}</div>
    </div>
    <div class="login_copyright">Copyright © 2022 Oboro month era All Rights Reserved.</div>
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
    },
    // login_up 方法名
    // url 访问的路径
    // method 访问的类型
    // then 成功执行方法
    // catch 失败执行方法
    login_up: function (e) {
      this.$axios({
        url: 'http://localhost:8080/login',
        method: 'post',
        data: {
          fdUser: this.userName,
          fdPassWord: this.passWord
        }
      })
        .then((res) => {
          if (res.data.code === '200') {
            this.$router.push('/index')
          } else {
            alert('用户名或密码错误！请重新填写正确用户名或密码')
          }
        })
        .catch((err) => {
          console.log(err)
        })
    }
  }
}
</script>
<!--scoped 只在此组件生效-->
<style scoped>
@import url('../assets/css/login/loginStyle.css');
</style>
