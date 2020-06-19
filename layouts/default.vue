<template>
  <div>
    <nuxt />
    <l-footer />
  </div>
</template>

<script>
import lFooter from "~/components/Footer";
import { firebase, db } from "~/plugins/firebase";
import { mapActions } from "vuex";
export default {
  components: {
    lFooter
  },
  created() {
    firebase.auth().onAuthStateChanged(user => {
      if (user) {
        this.setUser(user);
        db.collection("users")
          .doc(user.uid)
          .set({
            uid: user.uid,
            displayName: user.displayName,
            photoURL: user.photoURL
          });
      } else {
        this.setUser(null);
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
.el-upload {
  width: 100%;
}
</style>
