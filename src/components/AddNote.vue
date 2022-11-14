<template>
<div class="container">
    <h2>Create your Postit</h2>
    <router-link style="text-decoration: none; color: inherit;" to ="/"> <img src="./img/la-fleche.png"><h3>My Post-it</h3></router-link>
    <div class="c-note">
        <input  v-model="title" class="note" placeholder="postit title"> 
       <textarea cols="30" rows="10" v-model="content" class="note"></textarea>
       <button  class="note"  @click.prevent="addPost()">create</button>
    </div>
</div>
    
</template>
<script>
import axios from 'axios'
   export default {
    data(){
        return{
            title:'',
            content: []
        }
    },
    methods:{
        addPost(){
        const posts = {title: this.title, content: this.content };
        const headers = {
            "Content-Type": "application/json"
            };
            axios.post("http://5.135.119.239:3090/notes", posts, {headers})
            .then(response => this.note_id = response.data.note_id);
            this.$router.push('/');
        }
        
    }
    
   }
</script>
<style>
.container{
    height: 100vh;
    margin: 0 auto;
}
.c-note{
    margin: 0 auto;
    margin-top : 8vh;
    height: 50vh;
    display:flex;
    flex-direction: column;
    justify-content: center;
    width: 50%;
}
.note{
    margin-top:7vh;
    border: 4px solid black;
}
</style>
