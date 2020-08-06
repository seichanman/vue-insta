<template>
  <div>
    <div v-for="user in users" :key="user.id" class="users">
      <user :user="user" />
    </div>
  </div>
</template>

<script>
import User from "~/components/User.vue";
import { db } from "~/plugins/firebase";
export default {
  components: {
    User,
  },
  data() {
    return {
      users: [],
    };
  },
  async mounted() {
    const snapshot = await db.collection("users").get();
    snapshot.forEach((doc) => {
      this.users.push({ id: doc.id, ...doc.data() });
    });
  },
};
</script>

<style lang="scss">
.users {
  padding: 40px 6%;
  max-width: $container;
  margin: 0 auto;
}
</style>
