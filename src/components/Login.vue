<template>
    <div class="login_container">
        <div class="login_box">
            <div class="avatar_box">
                <img src="../assets/logo.png" alt/>
            </div>
            <el-form ref="loginFormRef" :model="loginForm"  :rules="loginRules" class="login_form" label-width="0">
                <el-form-item prop="username">
                    <el-input v-model="loginForm.username" prefix-icon="iconfont icon-denglu"></el-input>
                </el-form-item>
                <el-form-item prop="password">
                    <el-input v-model="loginForm.password" prefix-icon="iconfont icon-denglumima" type="password"></el-input>
                </el-form-item>
                <el-form-item  class="btns">
                    <el-button type="primary" @click="login()">提交</el-button>
                    <el-button type="info" @click="resetLoginFrom()">重置</el-button>
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
                    username: "admin",
                    password: "123456"
                },
                loginRules: {
                    username: [
                        { required: true, message: '请输入用户名称', trigger: 'blur' },
                        { min: 5, max: 20, message: '长度在 5 - 20 个字符', trigger: 'blur' }
                    ],
                    password: [
                        { required: true, message: '请输入密码', trigger: 'blur' },
                        { min: 5, max: 20, message: '长度在 5 - 20 个字符', trigger: 'blur' }
                    ],
                },
            }
        },
        methods: {
           resetLoginFrom(){
                this.$refs.loginFormRef.resetFields();
           },
           login(){
                this.$refs.loginFormRef.validate(async valid => {
                    if ( !valid ) return;
                    const {data:res} = await this.$http.post("login",this.loginForm)
                    if ( res.code == "200") {
                        this.$message.success("操作成功");
                        this.$router.push({path:"/home"});
                    } else {
                        this.$message.error("操作失败")
                    }
                    console.log(res);
                })
           }
        }
    }
</script>
<style lang="less" scoped>
.login_container{
    background-color: #2b4b6b;
    height: 100%;
}
.login_box{
    width: 450px;
    height: 300px;
    background-color: #fff;
    border-radius: 3px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
    .avatar_box{
        width: 130px;
        height: 130px;
        border: 1px solid #eee;
        border-radius: 50%;
        padding: 10px;
        box-shadow: 0 0 2px #ddd;
        position: absolute;
        left: 50%;
        transform: translate(-50%,-50%);
        background-color: #0ee;
        img{
            height: 100%;
            width: 100%;
            border-radius: 50%;
            background-color: #eee; 
        }
    }
}
.btns{
    display: flex;
    justify-content: flex-end;
}
.login_form{
    position: absolute;
    width: 100%;
    bottom: 0%;
    padding: 0 10px;
    box-sizing: border-box;
}
</style>