<template>
  <div class="page-field login">
    <div class="page-title">
      登陆
    </div>

    <div class="page-part form-body">
      <mt-field label="用户名" placeholder="请输入用户名" type="text" v-model="username"></mt-field>
      <mt-field label="密码" placeholder="请输入密码" type="password" v-model="password"></mt-field>
    </div>

    <div class="page-part form-button">
      <mt-button type="primary" class="form-submit" v-on:click="login()">登陆</mt-button>
      <mt-button type="default" v-on:click="register()">注册</mt-button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { Toast } from 'mint-ui';

export default {
  name: 'login',
  data() {
    return {
      username: '',
      password: '',
    };
  },
  methods: {
    login() {
      axios.post(`${process.env.BASE_URL}/user/login`, {
        username: this.username,
        password: this.password,
      }).then((response) => {
        if (response.status === 200) {
          if (response.data.code === 200) {
            Toast({
              message: '登陆成功',
              duration: 1500,
            });
            setTimeout(() => {
              this.$router.push({
                name: 'Index',
              });
            }, 1500);
          } else {
            Toast({
              message: response.data.message,
              duration: 1500,
            });
          }
        }
      }).catch((err) => {
        Toast({
          message: err.message,
          duration: 1500,
        });
      });
    },
    register() {
      this.$router.push({
        name: 'Register',
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.form-button {
  margin-top: 20px;
}

.form-submit {
  margin-right: 40px;
}

.form-body {
  margin-top: 20px;
}
</style>
