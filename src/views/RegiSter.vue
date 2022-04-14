<template>
  <div>
    <div class="f1">
      <div class="container">
        <span>创建新的账户</span>
        <div class="user">
          <label for="">用户名或电子邮件 *</label>
          <div>
            <input
              type="text"
              class="ru"
              v-model="username"
              @blur="checkForm()"
            />
          </div>
        </div>
        <div class="phone">
          <label for="">手机号</label>
          <div>
            <input
              type="text"
              class="sh"
              v-model="userphone"
              @blur="checkPhone()"
            />
          </div>
        </div>
        <div class="pwd">
          <label for="">密码</label>
          <div>
            <input
              type="password"
              class="ma"
              v-model="pwd"
              @blur="checkPwd()"
            />
          </div>
        </div>
        <div class="repwd">
          <label for="">确认密码</label>
          <input
            type="password"
            v-model="repwd"
            class="rz"
            @blur="checkRepwd()"
          />
        </div>
        <div class="mi">
          <button @click="checkHome()">注册</button>
          <div class="aa">
            <label for="">
              <input class="dd" type="checkbox" />
              接收来自我们的合作伙伴的报价
            </label>
          </div>
          <div class="foot">
            <label for="">已经有一个账号?</label>
            <button class="btn2" @click="goLogin">登录</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      pwd: "",
      repwd: "",
      userphone: "",
    };
  },
  methods: {
    goLogin() {
      this.$router.push({ path: "/login" });
    },
    checkForm() {
      //验证用户名
      let ert = /^\w{6,15}$/;
      if (ert.test(this.username)) {
        this.$message.success("用户名正确");
        return true;
      } else {
        this.$message.error("用户名不符合规定");
        return false;
      }
    },
    checkPhone() {
      //验证手机号
      let ect = /^1[3-9]\d{9}$/;
      if (ect.test(this.userphone)) {
        this.$message.success("手机号符合");
        return true;
      } else {
        this.$message.error("请输入正确手机号");
        return false;
      }
    },
    checkPwd() {
      //验证密码
      let ecx = /^[a-zA-Z]\w{5,17}$/;
      if (ecx.test(this.pwd)) {
        this.$message.success("密码符合");
        return true;
      } else {
        this.$message.error("密码不符合规定");
        return false;
      }
    },
    checkRepwd() {
      //验证密码是否一致
      if ((this.pwd = this.repwd)) {
        this.$message.success("注册通过");
        return true;
      } else {
        this.$message.error("请再次确认密码是否一致");
        return false;
      }
    },
    checkHome() {
      //多表验证
      if (
        this.checkForm() &&
        this.checkPhone() &&
        this.checkPwd() &&
        this.checkRepwd()
      ) {
        console.log("表单注册,执行注册");
        // /发送注册请求
        // let url = "/reist";
        // let params = `username=${this.username}&pwd=${this.pwd}&phone=${this.userphone}&repwd=${this.repwd}`
        this.axios
          .post(
            "/reist",
            `username=${this.username}&&pwd=${this.pwd}&&phone=${this.userphone}&&repwd=${this.repwd}`
          )
          .then((res) => {
            console.log("注册结果", res);
            if (res.data.code == 201) {
              this.$toast({
                message: "注册成功",
                position: "button",
                duration: 8080,
              });
              // 注册成功后跳转到登录页面
              this.$router.push({ path: "/login" });
            }
          });
      }
    },
  },
};
</script>
<style scoped src="../assets/css/register.css"></style>
<style lang="scss" scoped></style>
