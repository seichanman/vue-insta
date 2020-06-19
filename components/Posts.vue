<template>
  <div class="post">
    <post v-for="(post, index) in posts" :key="index" :post="post" />
    <div v-if="isAuthenticated && modalVisible" class="post-modal">
      <div class="post-modal__action">
        <div class="post-modal__action-arrow" @click="modalVisible = false">
          <img src="/images/back.svg" />
        </div>
        <div class="post-modal__action-btn" @click="post">Post</div>
      </div>
      <div class="post-modal__content">
        <div v-if="imageUrl" class="post-modal__content-img">
          <img :src="imageUrl" alt />
        </div>
        <el-upload v-if="!imageUrl" action :show-file-list="false" :http-request="uploadFile">
          <el-button class="post-modal__content-btn" size="small" type="primary">Click to upload</el-button>
        </el-upload>
        <el-input
          class="post-modal__content-text"
          type="textarea"
          :rows="8"
          placeholder="please input"
          v-model="text"
        ></el-input>
      </div>
    </div>
    <login v-else-if="!isAuthenticated && modalVisible" />
  </div>
</template>

<script>
import Login from "~/components/Login";
import Post from "~/components/Post.vue";
import { db, firebase } from "~/plugins/firebase";
import { mapGetters, mapState } from "vuex";

export default {
  data() {
    return {
      posts: [],
      imageUrl: null,
      text: null,
      modalVisible: false
    };
  },
  components: {
    Post,
    Login
  },
  computed: {
    ...mapGetters(["isAuthenticated"]),
    ...mapState(["user"])
  },
  methods: {
    async post() {
      await db.collection("posts").add({
        text: this.text,
        image: this.imageUrl,
        createdAt: new Date().getTime(),
        userId: this.user.uid
      });
      this.modalVisible = false;
      this.text = null;
      this.imageUrl = null;
      window.alert("保存されたよ");
    },
    openModal() {
      this.modalVisible = true;
    },
    async uploadFile(data) {
      const storageRef = firebase.storage().ref();
      const time = new Date().getTime();
      const ref = storageRef.child(`posts/${time}_${data.file.name}`);
      const snapshot = await ref.put(data.file);
      const url = await snapshot.ref.getDownloadURL();
      this.imageUrl = url;
    }
  },
  mounted() {
    //非同期処理
    db.collection("posts").orderBy('createdAt').onSnapshot(snapshot => {
    //orderBy('') = 順番の並び替え
      snapshot.docChanges().forEach(change => {
        const doc = change.doc;
        if (change.type === "added") {
          this.posts.unshift({ id: doc.id, ...doc.data() });
        }
      });
    });
  }
};
</script>

<style lang="scss" scoped>
.post {
  max-width: $container;
  margin: 0 auto;
  &-modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: #fff;
    z-index: 999;
    padding: 6%;
    &__action {
      display: flex;
      justify-content: space-between;
      width: 100%;
      max-width: 980px;
      margin: 0 auto;
      &-arrow {
        display: block;
        cursor: pointer;
      }
      &-btn {
        background: #333;
        border-radius: 15px;
        color: #fff;
        line-height: 30px;
        text-align: center;
        width: 70px;
        font-size: 1.4rem;
        cursor: pointer;
      }
    }
    &__content {
      width: 100%;
      max-width: 980px;
      margin: 0 auto;
      &-btn {
        display: block;
        width: 100%;
        margin-top: 40px;
        font-size: 1.6rem;
      }
      &-text {
        margin-top: 20px;
      }
    }
  }
}
</style>
