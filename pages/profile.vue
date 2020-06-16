<template>
  <div class="profile">
    <div class="profile__body">
      <div class="profile__head">
        <login
          class="profile__button"
          v-if="!isAuthenticated"
          :isAuthenticated="isAuthenticated"
        />
        <div class="profile__user">
          <template v-if="isAuthenticated">
            <div class="profile__userIcon">
              <img :src="user.photoURL" alt />
            </div>
            <span class="profile__name">{{ user.displayName }}</span>
          </template>
        </div>
        <button class="profile__button" @click="logout">ログアウト</button>
      </div>
      <div class="profile__info">
        <ul class="profile__items">
          <li class="profile__item">
            <span class="profile__title">post</span>
            <span class="profile__number">0</span>
          </li>
          <li class="profile__item">
            <span class="profile__title">following</span>
            <span class="profile__number">0</span>
          </li>
          <li class="profile__item">
            <span class="profile__title">follower</span>
            <span class="profile__number">0</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import Login from "~/components/Login";
import { firebase } from "~/plugins/firebase";
import { mapGetters, mapState } from "vuex";
export default {
  components: {
    Login
  },
  computed: {
    ...mapGetters(["isAuthenticated"]),
    ...mapState(["user"])
  },
  methods: {
    logout() {
      firebase.auth().signOut();
    }
  }
};
</script>

<style lang="scss" scoped>
.profile {
  padding: 40px 0;

  &__body {
    padding: 0 20px;
    max-width: 960px;
    margin: 0 auto;
  }

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
</style>
