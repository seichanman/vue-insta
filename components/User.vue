<template>
 <div class="user">
   <div class="user__info">
     <div class="user__avatar">
       <a><img src="/images/post1.jpg" class="user__image"></a>
     </div>
     <div class="user__name">
       <p>cohki0305</p>
     </div>
   </div>
   <div class="follow">
     <el-button class="follow__btn">Follow</el-button>
   </div>
 </div>
</template>

<style lang="scss" scoped>
  .user {
    align-items: center;
    display: flex;
    justify-content: space-between;
    &:nth-child(n + 2){
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
    }
    &__image {
      transform: translateY( -10%);
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
    }
  }
</style>