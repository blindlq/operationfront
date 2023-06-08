<template>
    <div class="login_container">
        <div class="login_box">
            <div class="avatar_box">
                <img src="../assets/logo.png" alt/>
            </div>
            <el-form ref="loginFormRef" :model="loginForm" class="login_form" label-width="0">
                <el-form-item >
                    <el-input v-model="loginForm.username"></el-input>
                </el-form-item>
                <el-form-item >
                    <el-input v-model="loginForm.password"></el-input>
                </el-form-item>
                <el-form-item  class="btns">
                    <el-button type="primary">提交</el-button>
                    <el-button type="info">重置</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                loginForm: {
                    username: "username",
                    password: "password"
                }
            }
        }
    }
</script>
<style lang="less" scoped>
</style>