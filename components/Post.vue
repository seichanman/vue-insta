<template>
    <div class="post-item">
        <div class="post-item__user">
            <div class="post-item__user-img">
                <a>
                    <img :src="user.photoURL" alt="">
                </a>
            </div>
            <div class="post-item__user-name">
                <p>{{ username }}</p>
            </div>
        </div>
        <figure class="post-item__img">
            <img :src="post.image" alt="">
        </figure>
        <div class="post-item__count">
            <img v-if="beLiked" class="post-item__count-img" src='/images/heart_active.svg'>
            <img v-else class="post-item__count-img" src='/images/heart.svg'>
            <p class="post-item__count-number">0</p>
        </div>
        <div class="post-item__text">
            <p>{{ post.text }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props:['post'],
    data(){
        return{
            user:{
                displayName:'siho',
                photoURL:'/images/post1.jpg'
            },
            beLiked:false
        }
    },
    computed:{
        username() {
            return this.user.displayName.charAt(0).toUpperCase() + this.user.displayName.slice(1);
        }
    }
}
</script>

<style lang="scss" scoped>
.post-item{
    &__user{
        display: flex;
        align-items: center;
        padding: 30px 20px 10px 20px;
        &-img{
            width: 30px;
            height: 30px;
            border-radius: 50%;
            overflow: hidden;
        }
        &-name{
            margin-left: 10px;
            font-weight: bold;
            font-size: 1.4rem;
        }
    }
    &__img{
        width: 100%;
    }
    &__count{
        display: flex;
        padding: 10px 20px;
        &-img{
        max-width: 24px;
        }
        &-number{
        margin-left: 15px;
        }
    }
    &__text{
        padding: 0 20px;
    }
}
</style>
