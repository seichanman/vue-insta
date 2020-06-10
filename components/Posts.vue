<template>
    <div class="post">
        <post v-for="(post,index) in posts" :key="index" :post="post.content" :user="post.user" :be-liked="post.beLiked" />
    </div>
</template>

<script>
import Post from '~/components/Post.vue'

export default {
    data(){
        return{
            posts:[
                {
                    user:{
                        displayName:'cohki0305',
                        photoURL:"/images/post0.jpg"
                    },
                    content:{
                        text:'恵比寿なう',
                        image:'/images/post0.jpg'
                    },
                    beLiked:true
                },{
                    user:{
                        displayName:'test user',
                        photoURL:"/images/post1.jpg"
                    },
                    content:{
                        text:'原宿なう',
                        image:'/images/post0.jpg'
                    },
                    beLiked:false
                }
            ]
        }
    },
    components: {
        Post
    }
}
</script>

<style lang="scss" scoped>
    .post{
        max-width: $container;
        margin: 0 auto;
    }
</style>
