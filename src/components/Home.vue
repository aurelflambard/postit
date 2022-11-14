<template>
  <h1>POST-IT</h1>
  <router-link style="text-decoration: none; color: inherit" to="/addNote"
    >CREATE A POSTIT<img src="./img/plus.png"
  /></router-link>
  <div class="posts">
    <div v-for="post in posts" :key="post" class="post">
      <div class="title">
        <h3>{{ post.title }}</h3>
      </div>
      <p v-for="content in post.content" :key="content">
        {{ content }}
      </p>
      <router-link :to="{ name: 'note', params: { _id: post._id } }">
        <img src="./img/fleche.png" alt=""
      /></router-link>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      posts: null,
    };
  },
  mounted() {
    const headers = { "Content-Type": "application/json" };
    axios
      .get("http://5.135.119.239:3090/notes", { headers })
      .then((reponse) => {
        this.posts = reponse.data.notes;
      });
  },
};
</script>
<style>
.posts {
  padding-top: 10vh;
  display: grid;
  margin: 0 auto;
  gap: 1rem;
}
.posts :nth-child(3n) {
  background-color: bisque;
}
.posts :nth-child(4n) {
  background-color: azure;
}

.post {
  padding: 1rem;
  background-color: rgb(240, 230, 140);
  box-shadow: 0px 10px 10px 10px grey;
  height: 35vh;
  margin: 10%;
}

/*RESPONSIVE*/
@media (min-width: 600px) {
  .posts {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 950px) {
  .posts {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>