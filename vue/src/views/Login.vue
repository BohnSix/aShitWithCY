<template>
  <div style="width: 100%; height: 100vh;background-color: aqua; overflow: hidden">
    <div style="width: 400px; margin: 150px auto ">
      <div style="color: #cccccc; font-size: 30px; text-align: center;padding: 30px 0">欢迎登陆</div>

      <el-form ref="form" :model="form" size="normal" :rules="rules">
        <el-form-item prop="username">
          <el-input prefix-icon="el-icon-user-solid" v-model="form.username"></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input prefix-icon="el-icon-lock" v-model="form.password" show-password></el-input>
        </el-form-item>
        <el-button type="primary" style="width: 100%" @click="login">登 录</el-button>
      </el-form>

    </div>
  </div>
</template>

<script>
import request from "../../utils/request";

export default {
  name: "Login",
  data() {
    return {
      form: {},
      rules: {
        username: [
          {require: true, message: "请输入用户名", trigger: "blur"}
        ],
        password: [
          {require: true, message: "请输入密码", trigger: "blur"}
        ]
      }
    }
  },
  methods: {
    login() {
      request.post("/api/user/login", this.form).then(res => {
        if (res.code === "0") {
          this.$message({
            type: "success",
            message: "登录成功"
          })
          this.$router.push("/")
        } else {
          this.$message({
            type: "error",
            message: res.msg
          })
        }
        this.load()
        this.dialogVisible = false
      })
    }
  }
}
</script>

<style scoped>

</style>