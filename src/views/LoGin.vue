<template>
  <div>
    <div class="f1">
      <div class="container">
        <span>登入你的账户</span>
        <div class="user">
          <label for="">用户名或电子邮件 *</label>
          <div><input type="text" class="ru" v-model="username" /></div>
        </div>
        <div class="pwd">
          <label for="">密码</label>
          <div><input type="password" class="ma" v-model="password" /></div>
        </div>
        <div class="mi">
          <button @click="goRein()">登录</button>
          <div class="aa">
            <label for="">
              <input class="dd" type="checkbox" />
              记得我
            </label>
            <router-link to="/" class="p">你的密码</router-link>
          </div>
          <div class="foot">
            <label for="">你没有账号?</label>
            <button class="btn2" @click="goReto()">现在创建账号</button>
            <button @click="getData()">获取数据</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "login",
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    getData() {
      this.axios.post("http://127.0.0.1:3000/v2/user/login").then((res) => {
        console.log(res);
      });
    },
    goReto() {
      this.$router.push({ path: "/reist" });
    },
    goRein() {
      if (!this.username) {
        this.$message.error("请输入用户名！");
        return;
      } else if (!this.password) {
        this.$message.error("请输入密码！");
        return;
      } else {
        //校验用户名和密码是否正确;
        this.$router.push({ path: "/home" });
        axios
          .post("./LoGin.vue", {
            name: this.username,
            password: this.password,
          })
          .then((res) => {
            // console.log("输出response.data.status", res.data.status);
            if (res.data.status === 201) {
              this.$router.push({ path: "/reist" });
            } else {
              alert("您输入的用户名或密码错误！");
            }
          });
      }
    },
  },
};
</script>

<style scoped src="../assets/css/login.css"></style>

<style lang="scss" scoped></style>
