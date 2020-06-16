<template>
  <div>
    <nuxt />
    <l-footer />
  </div>
</template>

<script>
import lFooter from "~/components/Footer";
export default {
  components: {
    lFooter
  }
};
</script>

<style lang="scss">
    .el-button {
        width: 100%;
    }
    .el-upload{
        width: 100%;
    }
</style>
