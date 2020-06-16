<template>
  <button @click="login">ログインする</button>
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

<style></style>
