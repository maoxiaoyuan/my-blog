<template>
    <div v-theme:column="'narrow'" id="show-blogs">
        <h1>博客总览</h1>
        <input type="text" v-model="search" placeholder="搜索">
        <div v-for="blog in filterdBlogs" class="single-blog">
            <router-link v-bind:to="'/blog/'+blog.id">
                <h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
            </router-link>  
            <article>
                {{blog.body | snippet}}
            </article>
        </div>
    </div>
  </template>
  
  <script>  
  export default {
    name: 'show-blogs',
    data(){
        return{
            blogs:[],
            search:""
        }                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             },
    created(){
         // this.$http.get("http://jsonplaceholder.typicode.com/posts")
        this.$http.get("./../static/posts.json")
        .then(function(data){
            // console.log(data)
            this.blogs=data.body.slice(0,10);
            // console.log(this.blogs)
        })
    },
    computed:{
        filterdBlogs:function(){
            return this.blogs.filter((blog)=>{
                return blog.title.match(this.search);
            })
        }
    },
    // 自定义过滤器
    filters:{
        "to-uppercase":function(value){
            return value.toUpperCase();
        },
        "snippet":function(value){
            return value.slice(0,100)+"..."
        }
    },
    // 自定义指令
    directives:{
        'rainbow':{
            bind(el,binding,vnode){
                el.style.color="#"+Math.random().toString(16).slice(2,8);
            }
        }
    }
    
  }
  </script>
  
  <style>
      #show-blogs{
          
          margin: 0 auto;
      }
      .single-blog{
          max-width: 800px;
          margin: 20px auto;
          padding:20px;
          box-sizing: border-box;
          background: #eee;
          border:1px dotted #aaa;
      }
      #show-blogs a{
          color:#444;
          text-decoration: none;
      }
      input[type="text"]{
          width:100%;
          height: 40px;
          box-sizing: border-box;
      }
  </style>
  