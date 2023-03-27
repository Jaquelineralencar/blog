<template>
  <div class="container">
    <h3 id="title">Destaques</h3>
    <div class="row">
      <div class="col-sm-6 mb-3 mb-sm-0" v-for="post in posts" :key="post.id">
        <div class="card" id="card">
          <div class="card-body">
            <h5 class="card-title"><b>{{ post.title }}</b></h5>
            <p class="card-text">{{ post.body }}</p>
            <a href="./comments">
              <button
                id="cardButton"
                @click="idPost(post)"
                class="btn btn-info"
              >
                Confira!
              </button></a
            >
          </div>
        </div>
      </div>
    </div>
  </div>
  <div id="pagePlus">
    <button type="button" class="btn btn-info" @click="paginationPage()">
      Exibir mais
    </button>
  </div>
</template>


<script>
import axios from "axios";
export default {
  name: "home",
  props: {
    posts: Array,
  },

  data() {
    return {
      posts: [],
      limitPage: 6,
      postId: 0,
    };
  },
  mounted() {
    this.getposts();
  },
  methods: {
    async getposts() {
      const response = await axios.get(
        `https://jsonplaceholder.typicode.com/posts?_start=0&_limit=${this.limitPage}`
      );
      if (response.status == 200) {
        this.posts = response.data;
      } else {
        console.error("Erro");
      }
    },

    paginationPage() {
      this.limitPage += 6;
      this.getposts();
    },

    idPost(post) {
      localStorage.setItem("idpost", post.id);
    },
  },
};
</script>

<style scoped>
#title {
  font-size: xx-large;
  font-family: cursive;
  text-align: center;
  padding: 1rem;
}

#card {
  width: 70%;
  margin: 3rem;

  background-color: rgba(228, 255, 246, 0.61);
}

#pagePlus {
  display: flex;
  justify-content: center;
  margin: 1rem;
}
#cardButton {
  width: 100%;
}
</style>