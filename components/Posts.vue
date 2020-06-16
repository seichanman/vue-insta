<template>
    <div class="post">
        <post v-for="(post,index) in posts" :key="index" :post="post" />
        <!--
        <div class="post-modal">
            <div class="post-modal__action">
                <div class="post-modal__action-s">
                    <img src="/images/back.svg" alt="">
                </div>
                <div class="post-modal__action-btn"></div>
            </div>
            <div class="post-modal__content">
                <el-upload action="" :show-file-list="false"
                :http-request="uploadFile">
                    <el-button size="small" type="primary"></el-button>
                </el-upload>
            </div>
        </div>
        -->
    </div>
</template>

<script>
import Post from '~/components/Post.vue'
import { db } from '~/plugins/firebase'

export default {
    data(){
        return{
            posts:[]
        }
    },
    components: {
        Post
    },
    methods:{
        uploadFile(data){
            debugger
        }
    },
    mounted(){//非同期処理
        db.collection('posts').onSnapshot((snapshot) => {
            snapshot.docChanges().forEach((change) => {
                const doc = change.doc
                if(change.type === 'added'){
                    this.posts.unshift({id:doc.id,...doc.data()})
                }
            })
        })
    }
}
</script>

<style lang="scss" scoped>
    .post{
        max-width: $container;
        margin: 0 auto;
        &-modal{
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: #fff;
            z-index: 999;
            padding: 6%;
        }
    }
</style>
