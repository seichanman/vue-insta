<template>
  <div class="login">
    <div class="login__logo">
      <img src="~/static/images/logo.png" alt />
    </div>
    <el-button class="login__button" @click="login" type="primary">ログインする</el-button>
  </div>
</template>

<script>
import { firebase } from "~/plugins/firebase";
import { mapState } from "vuex";

export default {
  methods: {
    async login() {
      const provider = new firebase.auth.GoogleAuthProvider();
      try {
        const result = await firebase.auth().signInWithPopup(provider);
      } catch (err) {
        alert("ログインしないの？" + err);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.login {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: #fff;
  z-index: 999;
  padding: 30% 6%;

  &__logo {
    text-align: center;
  }

  &__button {
    margin-top: 40px;
  }
}
</style>
