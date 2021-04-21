<template>
  <div class="container">
    <div class="form-body">
      <h2>注册账户</h2>
      <el-form
        :model="ruleForm2"
        status-icon
        :rules="rules2"
        ref="ruleForm2"
        label-width="0"
        class="demo-ruleForm"
      >
        <el-form-item  class="form-item">
          <el-input placeholder="请输入用户名" v-model="ruleForm2.username"></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input type="password" v-model="ruleForm2.password" auto-complete="off" placeholder="输入密码"></el-input>
        </el-form-item>
        <el-form-item prop="checkPass">
          <el-input type="password" v-model="ruleForm2.checkPass" auto-complete="off" placeholder="确认密码"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('ruleForm2')" style="width:100%;">注册</el-button>
          <p class="login" @click="gotoLogin">已有账号？立即登录</p>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Register",
  data() {
    // <!--验证密码-->
    let validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"))
      } else {
        if (this.ruleForm2.checkPass !== "") {
          this.$refs.ruleForm2.validateField("checkPass");
        }
        callback()
      }
    }
    // <!--二次验证密码-->
    let validatePass2 = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请再次输入密码"));
      } else if (value !== this.ruleForm2.password) {
        callback(new Error("两次输入密码不一致!"));
      } else {
        callback();
      }
    };
    return {
      ruleForm2: {
        username:"",
        password: "",
        checkPass: "",
      },
      rules2: {
        username: [{ validator: validatePass, trigger: 'change' }],
        password: [{ validator: validatePass, trigger: 'change' }],
        checkPass: [{ validator: validatePass2, trigger: 'change' }],
      }
    }
  },
  methods: {
    // <!--提交注册-->
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          setTimeout(() => {
            const _this = this;

            this.axios.post("/register",{
                username:this.ruleForm2.username,
                password:this.ruleForm2.password
              },
              alert("注册成功！"),
              this.$router.push({
                path: "/login"
              })
            )
              .then(function (response){
                console.log(response)
              }).catch(function (response){
              console.log(response)
            })
          }, 400);
        } else {
          console.log("error submit!!");
          return false;
        }
      })
    },
    // <!--进入登录页-->
    gotoLogin() {
      this.$router.push({
        path: "/login"
      });
    },
  }
};
</script>


<style scoped>
.container{
  height: 100%;
  width: 100%;
  /*background-image: url("../../static/bg.png");*/
  background-image: url("../../static/homeMask.png");
  background-size: cover;
  position: fixed;
  left: 0px;
  top:0px;
}
.form-body{
  border-radius: 10px;
  margin: 100px auto auto;
  width: 25%;
  min-width: 200px;
  padding: 30px 30px 15px 30px;
  background-color: rgba(255,255,255,0.8);
  box-shadow: 5px 3px 10px rgba(0,0,0,0.9);
}
.form-confirm{
  width: 100%;
  background-color: #585858;
  border: 2px solid #484848;
  border-radius: 4px;
}
.loading-wrapper {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background: #aedff8;
  display: flex;
  align-items: center;
  justify-content: center;
}
.register-wrapper img {
  position: absolute;
  z-index: 1;
}
.register-wrapper {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
}
#register {
  max-width: 340px;
  margin: 60px auto;
  background: #fff;
  padding: 20px 40px;
  border-radius: 10px;
  position: relative;
  z-index: 9;
}
.title {
  font-size: 26px;
  line-height: 50px;
  font-weight: bold;
  margin: 10px;
  text-align: center;
}
.el-form-item {
  text-align: center;
}
.login {
  margin-top: 10px;
  font-size: 14px;
  line-height: 22px;
  color: #1ab2ff;
  cursor: pointer;
  text-align: left;
  text-indent: 8px;
  width: 160px;
}
.login:hover {
  color: #2c2fd6;
}
.code >>> .el-form-item__content {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.code button {
  margin-left: 20px;
  width: 140px;
  text-align: center;
}
.el-button--primary:focus {
  background: #409EFF;
  border-color: #409EFF;
  color: #fff;
}
</style>
