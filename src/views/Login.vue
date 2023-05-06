<template>
    <div class="wrapper">
        <div class="login_box">
            <!-- 头像区域 -->
            <div class="avatar_box">
                <img
                        src="../assets/frontLogo.gif"
                        alt=""
                >
            </div>
        </div>
        <div style="margin: 250px auto; background-color: #fff; width: 450px; height: 320px; padding: 25px; border-radius: 10px">
            <div style="margin: 45px 0 20px 0; text-align: center; font-size: 24px"><b>登 录</b></div>
            <el-form :model="user" :rules="rules" ref="userForm">
                <el-form-item prop="username">
                    <el-input size="medium" placeholder="请输入用户名" style="margin: 10px 0" prefix-icon="el-icon-user"
                              v-model="user.username" @keyup.enter.native="login"></el-input>
                </el-form-item>
                <el-form-item prop="password">
                    <el-input size="medium" placeholder="请输入密码" style="margin: 10px 0" prefix-icon="el-icon-lock"
                              show-password
                              v-model="user.password" @keyup.enter.native="login"></el-input>
                </el-form-item>
                <el-form-item style="margin: 10px 0; text-align: right">
                    <el-button type="primary" size="small" autocomplete="off" @click="login">登录</el-button>
                    <el-button type="warning" size="small" autocomplete="off" @click="register">注册</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>

<script>
import {setRoutes} from "@/router";

export default {
    name: "Login",
    data() {
        return {
            user: {
                username: 'eilen',
                password: 'eilen',
            },
            rules: {
                username: [
                    {required: true, message: '请输入用户名', trigger: 'blur'},
                    {min: 3, max: 10, message: '长度在 3 到 5 个字符', trigger: 'blur'}
                ],
                password: [
                    {required: true, message: '请输入密码', trigger: 'blur'},
                    {min: 1, max: 20, message: '长度在 1 到 20 个字符', trigger: 'blur'}
                ],
            }
        }
    },
    methods: {
        register() {
            this.$router.push("/register")
        },
        login() {
            this.$refs['userForm'].validate((valid) => {
                if (valid) {  // 表单校验合法
                    this.request.post("/user/login", this.user).then(res => {
                        if (res.code === '200') {
                            localStorage.setItem("user", JSON.stringify(res.data))  // 存储用户信息到浏览器
                            localStorage.setItem("menus", JSON.stringify(res.data.menus))  // 存储用户信息到浏览器
                            // 动态设置当前用户的路由
                            setRoutes()
                            this.$message.success("登录成功")

                            if (res.data.role === 'ROLE_STUDENT') {
                                this.$router.push("/front/home")
                            } else {
                                this.$router.push("/")
                            }
                        } else {
                            this.$message.error(res.msg)
                        }
                    })
                }
            });
        }
    }
}
</script>

<style lang="less" scoped>
.wrapper {
  height: 100vh;
  background-image: linear-gradient(to bottom right, #FC466B, #3F5EFB);
  overflow: hidden;
}

.login_box {
  .avatar_box {
    width: 140px;
    height: 140px;
    border: 1px solid #eee;
    border-radius: 50%;
    padding: 10px;
    box-shadow: 0 0 10px #ddd;
    position: absolute;
    left: 50%;
    transform: translate(-50%, 120%);
    background-color: #fff;

    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #eee;
    }
  }
}
</style>