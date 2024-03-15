<template>
 <h2>這是後台!</h2>
 <RouterLink to="/admin/order">訂單列表</RouterLink> |
 <RouterLink to="/admin/products">產品訂單</RouterLink> |
 ||
 <RouterLink to="/">回到前台</RouterLink>
 <RouterView></RouterView>
</template>

<script>
import axios from 'axios';

const { VITE_URL } = import.meta.env;

export default {
  methods: {
    checkAdmin() {
      const api = `${VITE_URL}/v2/api/user/check`;
      axios.post(api)
        .then(() => {
        })
        // eslint-disable-next-line no-unused-vars
        .catch(() => {
          // alert(err.response.data.message);
          this.$router.push('/login');
        //   window.location = 'login.html';
        });
    },
  },
  mounted() {
    // 取得 Token（Token 僅需要設定一次）
    const token = document.cookie.replace(/(?:(?:^|.*;\s*)hexschoolToken\s*=\s*([^;]*).*$)|^.*$/, '$1');
    // token自動夾帶進去headers
    axios.defaults.headers.common.Authorization = token;

    this.checkAdmin();
  },
};
</script>
