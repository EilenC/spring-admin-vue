<template>
    <div class="wrapper">
        <div class="login_box">
            <!-- 头像区域 -->
            <div class="avatar_box">
                <img
                        src="../assets/LoginLogo.png"
                        alt=""
                >
            </div>
        </div>
        <div style="margin: 250px auto; background-color: #fff; width: 450px; height: 360px; padding: 25px; border-radius: 10px">
            <div style="margin: 45px 0 20px 0; text-align: center; font-size: 24px"><b>注  册</b></div>
            <el-form :model="user" :rules="rules" ref="userForm">
                <el-form-item prop="username">
                    <el-input placeholder="请输入账号" size="medium" style="margin: 5px 0" prefix-icon="el-icon-user" v-model="user.username"></el-input>
                </el-form-item>
                <el-form-item prop="password">
                    <el-input placeholder="请输入密码" size="medium" style="margin: 5px 0" prefix-icon="el-icon-lock" show-password v-model="user.password"></el-input>
                </el-form-item>
                <el-form-item prop="confirmPassword">
                    <el-input placeholder="请确认密码" size="medium" style="margin: 5px 0" prefix-icon="el-icon-lock" show-password v-model="user.confirmPassword"></el-input>
                </el-form-item>
                <el-form-item style="margin: 5px 0; text-align: right">
                    <el-button type="primary" size="small"  autocomplete="off" @click="login">注册</el-button>
                    <el-button type="warning" size="small"  autocomplete="off" @click="$router.push('/login')">返回登录</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>

<script>
export default {
    name: "Login",
    data() {
        return {
            user: {},
            rules: {
                username: [
                    { required: true, message: '请输入用户名', trigger: 'blur' },
                    { min: 3, max: 10, message: '长度在 3 到 5 个字符', trigger: 'blur' }
                ],
                password: [
                    { required: true, message: '请输入密码', trigger: 'blur' },
                    { min: 1, max: 20, message: '长度在 1 到 20 个字符', trigger: 'blur' }
                ],
                confirmPassword: [
                    { required: true, message: '请输入密码', trigger: 'blur' },
                    { min: 1, max: 20, message: '长度在 1 到 20 个字符', trigger: 'blur' }
                ],
            }
        }
    },
    methods: {
        login() {
            this.$refs['userForm'].validate((valid) => {
                if (valid) {  // 表单校验合法
                    if (this.user.password !== this.user.confirmPassword) {
                        this.$message.error("两次输入的密码不一致")
                        return false
                    }
                    this.request.post("/user/register", this.user).then(res => {
                        if(res.code === '200') {
                            this.$message.success("注册成功")
                            this.$router.push("/login")
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