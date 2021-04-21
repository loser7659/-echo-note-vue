<template>
  <div class="container">
    <div class="form-body">
      <h2>登录</h2>
      <el-form
        :model="loginForm"
        ref="loginForm"
        label-width="0"
        class="demo-ruleForm"
      >
        <el-form-item  class="form-item">
          <el-input placeholder="请输入用户名" v-model="loginForm.username"></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input type="password" v-model="loginForm.password" auto-complete="off" placeholder="输入密码"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('loginForm')" style="width:100%;">登录</el-button>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="toRegister()" style="width:100%;">注册</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Register",
  data() {
    return {
      loginForm: {
        username:"lee",
        password: "",
      }
    }
  },
  methods: {
    // <!--提交登录-->
    submitForm(formName) {
      const _this = this;
      this.axios.post("/login",{
        username:this.loginForm.username,
        password:this.loginForm.password,
      }).then(function (response){
        if(response.data.status === 200){
          // _this.$router.push({path: "/"})
          _this.$router.replace({
            path: '/',
          })
            .catch(()=>{});//把error 抛出来
          _this.$store.commit("login",response.data.object)
        }else{
          alert("账号或者密码错误")
        }


      }).catch(function (response){
        console.log(response)
      })
    },
    toRegister(){
      this.$router.replace('/register')
    }
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
