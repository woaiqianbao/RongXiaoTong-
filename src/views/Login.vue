<template>
  <div class="login-box">
    <div class="login">
      <img :src="require(`@/assets/img/yellowlogo.png`)" id="icon" >
      <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm" >
        <h2 >用户登录</h2>
        <el-form-item label="账号" prop="username" >
          <el-input  v-model="ruleForm.username" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="password">
          <el-input type="password" v-model="ruleForm.password" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="warning" @click="submitForm('ruleForm')">登录</el-button>
          <el-button  @click="resetForm('ruleForm')">重置</el-button>
        </el-form-item>
        <div style="text-align: right;color: white;">
          <el-link type="warning" style="margin-top: 20px" @click="$router.push('/register');">没有账号？去注册</el-link>
        </div>
      </el-form>




<!--      <div class="header">-->
<!--        -->
<!--        <h1>用户登录</h1>-->
<!--      </div>-->
<!--      <div id="login_form">-->
<!--        <div class="form-group">-->
<!--          <label for="username">帐号</label>-->
<!--          <input-->
<!--            type="text"-->
<!--            class="form-control"-->
<!--            id="username"-->
<!--            name="username"-->
<!--            placeholder="请输入账号"-->
<!--            v-model="acount"-->
<!--          />-->
<!--        </div>-->
<!--        <div class="form-group">-->
<!--          <label for="">密码</label>-->

<!--          <input-->
<!--            type="password"-->
<!--            class="form-control"-->
<!--            id=""-->
<!--            name="password"-->
<!--            placeholder="Password"-->
<!--            v-model="password"-->
<!--          />-->
<!--        </div>-->
<!--        <div class="checkbox">-->
<!--          <label> <input type="checkbox" />记住密码 </label>-->
<!--        </div>-->
<!--        <button class="btn btn-success btn-block" @click="loginBtn">-->
<!--          登录-->
<!--        </button>-->
<!--      </div>-->
<!--      <div class="message">-->
<!--        <p>没有账号? <router-link to="/register">立即注册</router-link></p>-->
<!--      </div>-->
    </div>
  </div>
</template>

<script>
import { userLogin } from "../api/user";
export default {
  name: "Login",
  data() {
    var validateUsername = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入用户名'));
      } else {
        callback();
      }
    };
    var validatePass = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入密码'));
      } else {

        callback();
      }
    };
    return {
      ruleForm: {
        username:'',
        password: '',
      },
      rules: {
        password: [
          { validator: validatePass, trigger: 'blur' }
        ],
        username:[
          { validator: validateUsername, trigger: 'blur' }
        ]
      }
    };
  },
  methods: {
    submitForm(formName) {

      this.$refs[formName].validate((valid) => {
        if (valid) {

          userLogin({
            username: this.ruleForm.username,
            password: this.ruleForm.password,
          }).then((res) => {

            if (res.flag == true) {
              // 在Vuex中存储token
              this.$store.commit("setToken", res.data);
              console.log( res.data)
              this.$router.push("/home").catch((err) => err);
            } else {
              alert(res.message);
            }
          }).catch((err) => {
            console.log(err);
          });
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
  },
  created() {},
};
</script>

<style lang="less" scoped>


.login-box {
  background-image: url("../assets/img/Login.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  position:absolute;
  left:0; top:0; width:100%;height:100%;
  box-sizing: border-box;
}


#icon{
  position:absolute;
  width: 100px;
  top:0%;
  left:50%;
  transform:translate(-50%,-50%);
}

.login{
  position:absolute;
  /*定位方式绝对定位absolute*/
  top:50%;
  left:80%;
  /*!*顶和高同时设置50%实现的是同时水平垂直居中效果*!*/
  transform:translate(-50%,-50%);
  /*实现块元素百分比下居中*/
  width:450px;
  min-height: 300px;
  padding-top:70px;
  padding-bottom:15px;
  padding-right:50px;

  background: rgba(0,0,0, .6);
  /*背景颜色为黑色，透明度为0.8*/
  box-sizing:border-box;
  /*box-sizing设置盒子模型的解析模式为怪异盒模型，
  将border和padding划归到width范围内*/
  box-shadow: 0px 15px 25px rgba(0,0,0,.5);
  /*边框阴影  水平阴影0 垂直阴影15px 模糊25px 颜色黑色透明度0.5*/
  border-radius:15px;
  /*边框圆角，四个角均为15px*/

  h2{
    margin-top: -10px;
    margin-bottom: 20px;
    padding:0;
    color: #fff;
    font-family: "PingFang SC";
    font-size: 24px;
    font-weight: bold;
    /*文字居中*/
    margin-left:44%
  }

  .inputbox{
    position:relative;
  }
}



.login .inputElement .el-input__wrapper{
  width: 100%;
  padding:5px 0;
  font-size:14px;
  color:white;
  letter-spacing: 1px;
  /*字符间的间距1px*/
  /*margin-bottom: 30px;*/
  border:none;
  border-bottom: 1px solid #fff;
  box-shadow: none;
  outline:none;
  /*outline用于绘制元素周围的线在这里用途,是将输入框的边框的线条使其消失*/
  background: transparent;
  /*背景颜色为透明*/
}

.login .inputElement .el-input__inner{
  font-size: 15px;
  color: #f6f0f0;
}

::v-deep .el-form-item__label{
  color: #dba155;
  font-family: 黑体;
  font-size: 17px;
  font-weight: bold;
}


</style>
