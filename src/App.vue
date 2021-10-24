<template>
  <div id="app">
    <h1>My Todos App</h1>
    <ui>
      <li v-for="post of posts" :key="post.id">{{post.title}}</li>
    </ui>
    <input type="text" v-model="postdata" @keyup.enter="addPost">

  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      posts:[],
      postdata:""

     }
  },
  async created(){
    try{
      let res=await axios.get("http://localhost:5000/api/post");
      this.posts=res.data.data

    }catch(e){
      console.error(e);
    }
  },
  methods:{
    async addPost(){
      try{
        let res = await axios.post("http://localhost:5000/api/post",{title:this.postdata});
        this.posts=[...this.posts,res.data.data];
        this.postdata="";
      }
      catch(e){
        console.error(e);
      }
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
