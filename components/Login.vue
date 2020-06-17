<template>
  <div class="login">
    <el-button @click="login">ログインする</el-button>
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
  padding: 6%;
}
</style>
