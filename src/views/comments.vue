<template>
  <div id="postDescription">
    <h5 class="card-title"><b>{{ posts.title }}</b></h5>
    <br />
    <p class="card-text">{{ posts.body }}</p>
    <p><b>Posted by {{ user.username }} </b></p>
  </div>

  <div class="comments">
    <h2>
      <b>Comentários ({{ comments.length }})</b>
    </h2>

    <div v-if="comments.length === 0">
      <p>Não há comentários ainda.</p>
    </div>

    <div v-else>
      <div id="commentsBody" v-for="comments in comments" :key="comments.id">
        <div>
          <b>{{ comments.userName }} </b>
        </div>

        <div>
          <b>{{ comments.name }} </b>
        </div>

        <div>{{ comments.body }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "comments",

  props: {
    comments: Array,
    userCommentsList: Array,
    user: Array,
  },
  data() {
    return {
      comments: [],
      posts: [],
      user: [],
      userCommentsList: [],
      idposts: localStorage.getItem("idpost"),
    };
  },
  mounted() {
    this.getComments();
    this.getPosts();
  },
  methods: {
    async getComments() {
      const response = await axios.get(
        `https://jsonplaceholder.typicode.com/post/${this.idposts}/comments`
      );
      if ((response.status = response.data)) {
        this.comments = response.data;
      } else {
        console.error("Erro");
      }
    },

    async getPosts() {
      const response = await axios.get(
        `https://jsonplaceholder.typicode.com/posts/${this.idposts}`
      );

      if ((response.status = response.data)) {
        this.posts = response.data;
      } else {
        console.error("Erro");
      }
      this.getUser(this.posts);
    },
    async getUser(postId) {
      const response = await axios.get(
        `https://jsonplaceholder.typicode.com/users/${postId.id}`
      );

      if ((response.status = response.data)) {
        this.user = response.data;
      } else {
        console.error("Erro");
      }
      this.getUserComment(this.comments);
    },
    async getUserComment() {
      var userList = [];
      for (let i = 0; i < this.comments.length; i++) {
        const response = await axios.get(
          `https://jsonplaceholder.typicode.com/users/${i == 0 ? 1 : i + 1}`
        );
        this.comments[i].userName = response.data.username;

        if ((response.status = response.data)) {
          this.userCommentsList = response.data;
          userList.push(this.userCommentsList);
        } else {
          console.error("Erro");
        }
      }
    },
  },
};
</script>

<style>
.comments {
  margin-top: 1px;
}
#postDescription {
  background-color: rgba(228, 255, 246, 0.61);
  text-align: center;
  margin: 2rem;
}
#commentsBody {
  margin: 1rem;
  padding: 0.5rem;
  background-color: rgb(255, 255, 255);
  border: 3px solid rgb(220, 245, 238);
  border-radius: 4%;
}
</style>