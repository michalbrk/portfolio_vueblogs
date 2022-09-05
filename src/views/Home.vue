<template>
  <div class="home">
    <Blogpost v-if="!userHome" :post="welcomeScreen"/>
    <Blogpost :post="post" v-for="(post, idx) in blogPostsFeed" :key="idx"/>
    <div class="blog-card-wrap">
      <div class="container">
        <h3>View More Recent Blogs</h3>
        <div class="blog-cards">
          <Blogcard :post="post" v-for="(post, idx) in blogPostsCards" :key="idx"/>
        </div>
      </div>
    </div>
    <div v-if="!userHome" class="updates">
      <div class="container">
        <h2>Never miss a post. Register for your free account today!</h2>
        <router-link class="router-button" to="#">
          Register for Vue Blog
          <Arrow class="arrow arrow-light"/>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import Blogpost from '../components/BlogPost.vue';
import Blogcard from '../components/BlogCard.vue';
import Arrow from '../assets/Icons/arrow-right-light.svg';

export default {
  name: "Home",
  components: { Blogpost, Blogcard, Arrow },
  data() {
    return {
      welcomeScreen: {
        title: "Welcome!",
        blogPost: "Enim cillum nostrud reprehenderit reprehenderit sunt fugiat laboris esse esse sunt sint deserunt aliqua. Esse proident adipisicing nisi officia duis nisi anim ipsum tempor sit. Sit tempor cillum anim non veniam occaecat cupidatat laborum ipsum ipsum aliquip in. Deserunt laborum consequat eiusmod exercitation sint sit consectetur ut ea consequat.",
        isWelcomeScreen: true,
        photo: "coding"
      }
    }
  },
  computed: {
    blogPostsFeed(){
      return this.$store.getters.blogPostsFeed;
    },
    blogPostsCards(){
      return this.$store.getters.blogPostsCards;
    },
    userHome(){
      return this.$store.state.user;
    }
  }
};
</script>
<style lang="scss" scoped>
.blog-card-wrap {
  h3 {
    font-weight: 300;
    font-size: 28px;
    margin-bottom: 32px;
  }
}

.updates {
  .container {
    padding: 100px 25px;
    display: flex;
    flex-direction: column;
    align-items: center;
    @media (min-width: 800px) {
      padding: 125px 25px;
      flex-direction: row;
    }

    .router-button {
      display: flex;
      font-size: 14px;
      text-decoration: none;
      @media (min-width: 800px) {
        margin-left: auto;
      }
    }

    h2 {
      font-size: 32px;
      font-weight: 300;
      width: 100%;
      max-width: 425px;
      text-align: center;
      text-transform: uppercase;
      @media (min-width: 800px) {
        text-align: initial;
        font-size: 40px;
      }
    }
  }
}
  
</style>
