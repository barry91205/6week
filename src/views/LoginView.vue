<template>
    <h2>這是燈入夜面!</h2>
    <div class="container">
        <div class="row justify-content-center border rounded p-5">
          <h1 class="h3 mb-3 font-weight-normal">
            請先登入
          </h1>
          <div class="col-8">
            <form id="form" class="form-signin" @submit.prevent="login">
              <div class="form-floating mb-3">
                <input type="email" class="form-control" id="floatingInput"
                  placeholder="name@example.com" required autofocus v-model="user.username">
                <label for="floatingInput">Email address</label>
              </div>
              <div class="form-floating">
                <input type="password" class="form-control" id="floatingPassword"
                  placeholder="Password" required v-model="user.password">
                <label for="floatingPassword">Password</label>
              </div>
              <button class="btn btn-lg btn-primary w-100 mt-3" type="submit" @click="login">
                登入
              </button>
            </form>
          </div>
        </div>
        <p class="mt-5 mb-3 text-muted">
          &copy; 2021~∞ - 六角學院
        </p>
      </div>
    <RouterView></RouterView>
</template>

<script>
import axios from 'axios';

const { VITE_URL } = import.meta.env;

export default {
  data() {
    return {
      user: {
        username: '',
        password: '',
      },
    };
  },
  methods: {
    login() {
      const api = `${VITE_URL}/v2/admin/signin`;
      // eslint-disable-next-line no-undef
      axios.post(api, this.user)
        .then((response) => {
          const { token, expired } = response.data;
          document.cookie = `hexschoolToken=${token};expires=${new Date(expired)}`;
          this.$router.push('./admin');
        }).catch(() => {
          // eslint-disable-next-line no-alert
          alert('帳號或密碼錯誤，請重新登入！');
        });
    },
  },
};
</script>
