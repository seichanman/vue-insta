<template>
  <div class="user">
    <div class="user__info">
      <div class="user__avatar">
        <nuxt-link :to="`/users/${user.uid}`">
          <img :src="user.photoURL" />
        </nuxt-link>
      </div>
      <div class="user__name">
        <p>{{ user.displayName }}</p>
      </div>
    </div>
    <div class="follow" v-if="!isCurrentUser">
      <el-button class="follow__btn" v-if="!followed" @click="follow">Follow</el-button>
      <el-button class="follow__btn active" v-else @click="unfollow">Unfollow</el-button>
    </div>
  </div>
</template>

<script>
import { db } from "~/plugins/firebase";
export default {
  data() {
    return {
      followed: false,
    };
  },
  props: ["user"],
  computed: {
    currentUser() {
      return this.$store.state.user;
    },
    isCurrentUser() {
      return this.currentUser.uid === this.user.id;
    },
  },
  async mounted() {
    this.followingRef = db
      .collection("users")
      .doc(this.currentUser.uid)
      .collection("followings")
      .doc(this.user.id);
    this.followerRef = db
      .collection("users")
      .doc(this.user.id)
      .collection("followers")
      .doc(this.currentUser.uid);
    const doc = await this.followingRef.get();
    this.followed = doc.exists;
  },
  methods: {
    async follow() {
      await this.followingRef.set({ user: this.user.id });
      await this.followerRef.set({ user: this.currentUser.uid });
      this.followed = true;
    },
    async unfollow() {
      await this.followingRef.delete();
      await this.followerRef.delete();
      this.followed = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.user {
  align-items: center;
  display: flex;
  justify-content: space-between;
  &:nth-child(n + 2) {
    padding-top: 20px;
  }
  &__info {
    align-items: center;
    display: flex;
  }
  &__avatar {
    border-radius: 50%;
    height: 50px;
    margin-right: 10px;
    overflow: hidden;
    width: 50px;
    img{
      height: 100%;
      object-fit: cover;
    }
  }
  &__image {
    transform: translateY(-10%);
  }
  &__name {
    font-size: 1.4rem;
    font-weight: bold;
  }
}
.follow {
  &__btn {
    background-color: #fff;
    font-size: 1.4rem;
    &.active{
      background:#3490dc ;
      color: #fff;
      border: none;
    }
  }
}
</style>
