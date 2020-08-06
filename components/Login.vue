<template>
  <div class="login">
    <div class="login__logo">
      <img src="~/static/images/logo.png" alt />
    </div>
    <el-button class="login__button" @click="$emit('login')" type="primary">ログインする</el-button>
  </div>
</template>

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
