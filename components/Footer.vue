<template>
  <footer class="footer">
    <div class="footer__body">
      <div class="footer__buttons">
        <div class="footer__button">
          <img src="~/static/images/home.svg" alt class="footer__icon" />
        </div>
        <div class="footer__button">
          <img src="~/static/images/follow.svg" alt class="footer__icon" />
        </div>
        <div class="footer__button">
          <img src="~/static/images/profile.svg" alt class="footer__icon" />
        </div>
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
  width: 100%;
  background-color: $white;
  border-top: 1px solid $gray-4;
  &__body {
    padding: 10px 40px;
    max-width: 960px;
    margin: 0 auto;
  }

  &__buttons {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  &__button {
  }

  &__icon {
    vertical-align: bottom;
  }
}
</style>