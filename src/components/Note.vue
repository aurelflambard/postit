<template>
    <div class="monPost">

        <router-link style="text-decoration: none; color: inherit; margin-top: 5vh" to="/"><img
                src="./img/fleche-gauche.png" alt="">BACK TO MY POSTIT</router-link>
        <div class="post1">
            <h2>{{ post?.title }}</h2>
            <p v-for="content in post?.content" :key="content">
                {{ content }}
            </p>
            <button class="delete" @click.prevent="deletePost()">DELETE</button>
            <router-link :to="{ name: 'editNote', params: { id: _id } }">EDIT</router-link>
        </div>

    </div>
</template>
<style>
.monPost {
    margin: 0 auto;
    display: flex;
    justify-content: center;
    height: 100vh;
}

.post1 {
    padding: 1rem;
    background-color: rgb(240, 230, 140);
    box-shadow: 0px 10px 10px 10px grey;
    height: 50vh;
    margin-top: 25vh;
    margin-right: 8%;
    width: 40%;
    display: flex;
    flex-direction: column;
}

.delete {
    margin-top: 4vh;
}
</style>
<script>
import axios from 'axios'
export default {
    props: ['_id'],
    data() {
        return {
            post: null,
        }
    },
    mounted() {
        const headers = { "Content-Type": "application/json" };
        axios.get("http://5.135.119.239:3090/notes/" + this.$route.params._id, { headers })
            .then((reponse) => {
                this.post = reponse.data.note;
                console.log(this.post)
            });
    },
    methods: {
        deletePost() {
            const deleted = {
                method: 'DELETE',
                headers: {
                    "Content-Type": "application/json"
                }
            };
            fetch("http://5.135.119.239:3090/notes/" + this.$route.params._id, deleted)
            this.$router.push('/');
        }
    }
}
</script>