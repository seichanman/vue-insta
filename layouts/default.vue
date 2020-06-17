<template>
  <div>
    <nuxt />
    <l-footer />
  </div>
</template>

<script>
import lFooter from "~/components/Footer";
import { firebase } from "~/plugins/firebase";
import { mapActions } from "vuex";
export default {
  components: {
    lFooter
  },
  created() {
    firebase.auth().onAuthStateChanged(user => {
      if (user) {
        this.setUser(user);
        console.log(user);
      } else {
        this.setUser();
      }
    });
  },
  methods: {
    ...mapActions(["setUser"])
  }
};
</script>

<style lang="scss">
    .el-button {
        width: 100%;
    }
    .el-upload{
        width: 100%;
    }
</style>
