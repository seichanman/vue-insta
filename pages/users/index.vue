<template>
 <div class="users">
   <user />
   <user />
 </div>
</template>

<script>
import User from '~/components/User.vue'
export default {
 components: {
   User
 }
}
</script>

<style lang="scss">
  .users{
    padding: 40px 6%;
    max-width: $container;
    margin: 0 auto;
  }
</style>