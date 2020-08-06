<template>
  <div class="profile">
    <div class="profile__head">
      <div class="profile__user">
        <template v-if="isAuthenticated">
          <div class="profile__userIcon">
            <img :src="userData.photoURL" alt />
          </div>
          <span class="profile__name">{{ userData.displayName }}</span>
        </template>
      </div>
      <el-button v-if="isCurrentUser" @click="logout">ログアウト</el-button>
    </div>
    <div class="profile__info">
      <ul class="profile__items">
        <li class="profile__item">
          <span class="profile__title">post</span>
          <span class="profile__number">{{ posts.length }}</span>
        </li>
        <li class="profile__item">
          <span class="profile__title">following</span>
          <span class="profile__number">{{ followingCount }}</span>
        </li>
        <li class="profile__item">
          <span class="profile__title">follower</span>
          <span class="profile__number">{{ followerCount }}</span>
        </li>
      </ul>
    </div>
    <post v-for="post in posts" :key="post.id" :post="post" :mode="'profile'" />
  </div>
</template>

<script>
import { firebase, db } from "~/plugins/firebase";
import { mapGetters, mapState } from "vuex";
import Post from "~/components/Post";
export default {
  data() {
    return {
      followingCount: 0,
      followerCount: 0,
      userData: {},
      posts: [],
    };
  },
  components: {
    Post,
  },
  async mounted() {
    const userId = this.$route.params.id;
    const doc = await db.collection("users").doc(userId).get();
    this.userData = doc.data();

    const snapshot = await db
      .collection("posts")
      .where("userId", "==", userId)
      .get();
    snapshot.forEach((doc) => {
      this.posts.push({ id: doc.id, ...doc.data() });
    });

    this.fetchFollowingCount();
    this.fetchFollowerCount();
  },
  computed: {
    ...mapGetters(["isAuthenticated"]),
    ...mapState(["user"]),
    isCurrentUser() {
      if (this.user) {
        return this.user.uid == this.$route.params.id;
      }
    },
  },
  methods: {
    async fetchFollowingCount() {
      const userId = this.$route.params.id;
      const snap = await db
        .collection("users")
        .doc(userId)
        .collection("followings")
        .get();
      this.followingCount = snap.size;
    },
    async fetchFollowerCount() {
      const userId = this.$route.params.id;
      const snap = await db
        .collection("users")
        .doc(userId)
        .collection("followers")
        .get();
      this.followerCount = snap.size;
    },
    logout() {
      firebase.auth().signOut();
    },
  },
};
</script>

<style lang="scss" scoped>
.profile {
  padding: 40px 6%;
  max-width: $container;
  margin: 0 auto;

  &__head {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  &__user {
    display: flex;
    align-items: center;
  }

  &__userIcon {
    > img {
      width: 40px;
      height: 40px;
      border-radius: 100%;
      object-fit: cover;
      vertical-align: bottom;
    }
  }

  &__name {
    margin-left: 10px;
  }

  &__button {
    background-color: $white;
    border: 1px solid $gray-4;
    font-size: 1.4rem;
    padding: 8px 10px;
  }

  &__info {
    margin-top: 40px;
  }

  &__items {
    display: flex;
    justify-content: space-between;
  }

  &__item {
  }

  &__title {
    display: block;
  }

  &__number {
    display: block;
    text-align: center;
  }
}

.el-button {
  width: auto;
}
</style>
