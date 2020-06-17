<template>
  <footer class="footer">
    <div class="footer__body">
      <div class="footer__buttons">
        <nuxt-link to="/" class="footer__button">
          <img src="~/static/images/home.svg" alt class="footer__icon" />
        </nuxt-link>
        <nuxt-link to="/users" class="footer__button">
          <img src="~/static/images/follow.svg" alt class="footer__icon" />
        </nuxt-link>
        <nuxt-link to="/profile" class="footer__button">
          <img src="~/static/images/profile.svg" alt class="footer__icon" />
        </nuxt-link>
      </div>
    </div>
  </footer>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100vw;
  background-color: $white;
  border-top: 1px solid $gray-4;
  z-index: 1000;
  &__body {
    max-width: $container;
    margin: 0 auto;
  }
  &__buttons {
    padding: 10px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  &__button {
    width: calc(100% / 3);
    display: flex;
    justify-content: center;
  }

  &__icon {
    vertical-align: bottom;
    max-width: 24px;
    max-height: 24px;
  }
}
</style>
