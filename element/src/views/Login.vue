<template>
    <div class="login-box">
        <el-form :model="loginData" status-icon :rules="rules" ref="loginForm">
            <el-form-item >
                <span class="title">Lemmer</span>
            </el-form-item>
            <el-form-item label="用户名" prop="username">
                <el-input v-model="loginData.username"
                          autocomplete="off"
                          placeholder="请输入用户名"
                          clearable></el-input>
            </el-form-item>
            <el-form-item label="密码" prop="password">
                <el-input type="password" v-model="loginData.password"
                          autocomplete="off"
                          placeholder="请输入密码"
                          show-password></el-input>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="submitForm('loginForm')">立即登录</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>

<script>
export default {
    name: "Login",
    data() {
        var validatePass = (rule, value, callback) => {
            if (value === '') {
                callback(new Error('请输入密码'));
            } else {
                if (this.ruleForm.checkPass !== '') {
                    this.$refs.ruleForm.validateField('checkPass');
                }
                callback();
            }
        };
        var validatePass2 = (rule, value, callback) => {
            if (value === '') {
                callback(new Error('请再次输入密码'));
            } else if (value !== this.ruleForm.pass) {
                callback(new Error('两次输入密码不一致!'));
            } else {
                callback();
            }
        };
        return {
            loginData: {
                username: '',
                password: ''
            },
            rules: {
                pass: [
                    {validator: validatePass, trigger: 'blur'}
                ],
                checkPass: [
                    {validator: validatePass2, trigger: 'blur'}
                ],
            }
        };
    },
    methods: {
        submitForm(formName) {
            this.$refs[formName].validate((valid) => {
                if (valid) {
                    alert('submit!');
                } else {
                    console.log('error submit!!');
                    return false;
                }
            });
        },
        resetForm(formName) {
            this.$refs[formName].resetFields();
        }
    }
}
</script>

<style scoped>
.login-box {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
}
.el-form{
    border: 1px solid #dfdfdf;
    width: 400px;
    padding: 30px;
}
.title{
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 26px;
}
.el-button{
    width: 100%;
}
</style>