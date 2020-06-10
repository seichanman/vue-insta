<template>
  <div>
    <header class="header">
      <div class="header__container">
        <div class="header__logo">
          <img src="/images/logo.png" class="">
        </div>
        <img class="header__post" src="/images/letter.svg">
      </div>
    </header>
    <div class="container">
      <posts />
    </div>
  </div>
</template>

<script>

import Posts from '~/components/Posts.vue'
export default {
 components: {
   Posts
 }
}
</script>

<style lang="scss" scoped>
  .header{
    border: 1px solid #ddd;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 999;
    background: #fff;
    &__container{
      position: relative;
      max-width: $container;
      margin: 0 auto;
      padding:10px 20px;
    }
    &__logo{
      margin: 0 auto;
      max-width: 80px;
      img{
        display: flex;
        align-items: center;
      }
    }
    &__post{
      position: absolute;
      top: 50%;
      right: 20px;
      transform: translateY(-50%);
      max-width: 24px;
    }
  }
  .container{
    margin:50px 0 52px;
  }
</style>
