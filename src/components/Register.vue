<template>
  <div class="page-field login">
    <div class="page-title">
      注册
    </div>

    <div class="page-part form-body">
      <mt-field label="用户名" placeholder="请输入用户名" type="text" v-model="username"></mt-field>
      <mt-field label="密码" placeholder="请输入密码" type="password" v-model="password"></mt-field>
    </div>

    <div class="page-part form-button">
      <mt-button type="primary" class="form-submit" v-on:click="register()">注册</mt-button>
      <mt-button type="default" v-on:click="login()">登陆</mt-button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { Toast } from 'mint-ui';

const BASE_URL = 'http://115.28.180.202:3000/';

export default {
  name: 'register',
  data() {
    return {
      username: '',
      password: '',
    };
  },
  methods: {
    register() {
      axios.post(`${BASE_URL}user/create_user`, {
        username: this.username,
        password: this.password,
      }).then((response) => {
        if (response.status === 200) {
          if (response.data.code === 200) {
            Toast({
              message: '注册成功,请登陆',
              duration: 1500,
            });
            setTimeout(() => {
              this.$router.push({
                name: 'Login',
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
          message: err,
          duration: 1500,
        });
      });
    },
    login() {
      this.$router.push({
        name: 'Login',
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a {
  color: #42b983;
}

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
