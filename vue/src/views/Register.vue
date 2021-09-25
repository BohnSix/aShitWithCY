<template>
  <div style="width: 100%; height: 100vh;background-color: aqua; overflow: hidden">
    <div style="width: 400px; margin: 150px auto ">
      <div style="color: #cccccc; font-size: 30px; text-align: center;padding: 30px 0">欢迎注册</div>

      <el-form ref="form" :model="form" size="normal" :rules="rules">
        <el-form-item prop="username">
          <el-input prefix-icon="el-icon-user-solid" v-model="form.username"
                     placeholder="请输入用户名"></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input prefix-icon="el-icon-lock" v-model="form.password"
                    show-password placeholder="请输入密码"></el-input>
        </el-form-item>
        <el-form-item prop="confirm" >
          <el-input prefix-icon="el-icon-lock" v-model="form.confirm"
                    show-password placeholder="请再次输入密码"></el-input>
        </el-form-item>
        <el-button type="primary" style="width: 100%" @click="register">注册</el-button>
      </el-form>

    </div>
  </div>
</template>

<script>
import request from "../../utils/request";

export default {
  name: "Register",
  data() {
    return {
      form: {},
      rules: {
        username: [
          {require: true, message: "请输入用户名", trigger: "blur"},
        ],
        password: [
          {require: true, message: "请输入密码", trigger: "blur"},
        ],
        confirm: [
          {require: true, message: "请再次输入密码", trigger: "blur"},
        ]
      }
    }
  },
  methods: {
    register() {
      if (this.form.password != this.form.confirm) {
        this.$message({
          type: "error",
          message: "两次密码输入不一致"
        })
      }
      request.post("/api/user/register", this.form).then(res => {
        this.$refs['form'].validate((valid) => {
          if (valid) {
            if (res.code === "0") {
              this.$message({
                type: "success",
                message: "注册成功"
              })
              this.$router.push("/login")
            } else {
              this.$message({
                type: "error",
                message: res.msg
              })
            }
            this.load()
            this.dialogVisible = false
          }
        })
      })
    }
  }
}
</script>

<style scoped>

</style>