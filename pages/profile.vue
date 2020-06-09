<template>
  <div class="profile">
    <div class="profile__head">
      <div class="profile__user">
        <div class="profile__icon">
          <img src="~/static/images/post1.jpg" alt />
        </div>
        <span class="profile__name">user-name</span>
      </div>
      <button class="profile__button">ログアウト</button>
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
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.profile {
  padding: 40px 20px;

  &__head {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  &__user {
    display: flex;
    align-items: center;
  }
  &__icon {
    width: 40px;
    height: 40px;
    border-radius: 100%;
    overflow: hidden;
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