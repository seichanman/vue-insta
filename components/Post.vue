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
            <img v-if="beLiked" @click="unlike" class="post-item__count-img" src='/images/heart_active.svg'>
            <img v-else @click="like" class="post-item__count-img" src='/images/heart.svg'>
            <p class="post-item__count-number">{{likeCount}}</p>
        </div>
        <div class="post-item__text">
            <p>{{ post.text }}</p>
        </div>
    </div>
</template>

<script>
import { db } from '~/plugins/firebase'

export default {
    props:['post'],
    data(){
        return{
            user:{
                displayName:'siho',
                photoURL:'/images/post1.jpg'
            },
            beLiked:false,
            likeCount:0
        }
    },
    mounted(){
        this.likeRef = db.collection('posts').doc(this.post.id).collection('likes')
        this.checkLikeStatus()
        this.likeRef.onSnapshot((snap)=>{
            this.likeCount = snap.size
        })

    },
    methods: {
        async like() {
            // async = 非同期関数を定義する関数宣言のこと。
            // 以下のように関数の前にasyncを宣言することにより、非同期関数（async function）を定義できる。
            await this.likeRef.doc(this.currentUser.uid).set({ uid: this.currentUser.uid})
            this.beLiked = true
            //await = async function内でPromiseの結果（resolve、reject）が返されるまで待機する（処理を一時停止する）演算子のこと。
            //likeRefのPromiseの結果が返ってくるまで以下は実行されない
            //add =  ドキュメントのIDを指定せずに保存する firebase側で適当につける
            //set = idを指定してドキュメンを追加する際に使用
        },
        async unlike(){
            await this.likeRef.doc(this.currentUser.uid).delete()
            this.beLiked = false
        },
        async checkLikeStatus(){
            const doc = await this.likeRef.doc(this.currentUser.uid).get()
            this.beLiked = doc.exists
        }
    },
    computed:{
        currentUser(){
            return this.$store.state.user
        },
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
    &__img,& img{
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


