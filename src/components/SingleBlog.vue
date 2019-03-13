<template>
    <div id="single-blog">
        <h1>{{blog.title}}</h1>
        <article>{{blog.body}}</article>
        <button v-on:click="deleteSingleBlog">删除</button>
        <router-link v-bind:to="'/edit/'+id">编辑</router-link>
    </div>
</template>
<script>
 export default{
     name:"single-blog",
     data(){
         return{
             id:this.$route.params.id,
             blog:{}
         }
     },
     created(){
         this.$http.get("http://jsonplaceholder.typicode.com/posts/"+this.id)
         .then(function(data){
             console.log(data);
            this.blog=data.body;
             
         })
     },
     methods:{
        deleteSingleBlog(){
            this.$http.delete("http://jsonplaceholder.typicode.com/posts/"+this.id)
                .then(Response=>{
                    this.$router.push({path:"/"})
                })
        }
     }
 }
</script>
<style>
#single-blog{
    max-width: 960px;
    margin:0 auto;
    padding:20px;
    background: #eee;
    border: 1px dotted #aaa;
}
</style>