<template>
        <div id="add-blog">
          <h2>编辑博客</h2>
          <form action="" v-if="!submitted">
              <label for="">博客标题</label>
              <input type="text" v-model="blog.title" required>
              <label for="">博客内容</label>
              <textarea v-model="blog.body"></textarea>
              <div id="checkboxes">
                  <label for="">Vue.js</label>
                  <input type="checkbox" value="Vue.js" v-model="blog.categories">
                  <label for="">Node.js</label>
                  <input type="checkbox" value="Node.js" v-model="blog.categories">
                  <label for="">React.js</label>
                  <input type="checkbox" value="React.js" v-model="blog.categories">
                  <label for="">Angular4.js</label>
                  <input type="checkbox" value="Angular4.js" v-model="blog.categories">
              </div>
              <label for="">作者</label>
              <select v-model="blog.author">
                  <option v-for="author in authors">
                      {{author}}
                  </option>
              </select>
              <button v-on:click.prevent="post">编辑博客</button>
          </form>
          <div v-if="submitted">
              <h3>您已成功添加博客！</h3>
          </div>
         <div id="preview">
             <h3>博客总览</h3>
             <p>博客标题：{{blog.title}}</p>
             <p>博客内容：</p>
             <p>{{blog.content}}</p>
             <p>博客分类</p>
             <ul>
                 <li v-for="category in blog.categories">
                     {{category}}
                 </li>
             </ul>
             <p>作者：{{blog.author}}</p>
         </div>
        </div>
      </template>
      
      <script>
      export default {
        //   http://jsonplaceholder.typicode.com/posts
        name: 'add-blog',
        data () {
          return {
            id:this.$route.params.id,
            blog:{},
            authors:["毛小园","丫头","放下曾经"],
            submitted:false
          }
        },
        methods:{
            fetchData(){
                this.$http.get("http://jsonplaceholder.typicode.com/posts/"+this.id)
                .then(Response=>{
                    this.blog=Response.body;
                })
            },
            post:function(){
                this.$http.put("http://jsonplaceholder.typicode.com/posts/"+this.id,this.blog).then(function(data){
                    console.log(data);
                    this.submitted=true;
                
                })
            }
        },
        created(){
            this.fetchData();
        }
      }
      </script>
      
      <!-- Add "scoped" attribute to limit CSS to this component only -->
      <style scoped>
      #add-blog *{
          box-sizing: border-box;
      }
      #add-blog{
          margin:20px auto;
          max-width: 600px;
          padding: 20px;
      }
      label{
          display: block;
          margin:20px 0 10px;
    
      }
      input[type="text"],textarea,select{
          display: block;
          width:100%;
          padding: 8px;
      }
      textarea{
          height: 200px;
      }
      #checkboxes label{
          display: inline-block;
          margin-top: 0;
      }
      #checkboxes input{
          display: inline-block;
          margin-right: 10px;
      }
      button{
          display: block;
          margin: 20px 0;
          background: crimson;
          border:0;
          color:#fff;
          border-radius: 4px;
          padding: 14px;
          font-size: 18px;
          cursor:pointer;
      }
      #preview{
          padding:10px 20px;
          border:1px dotted #ccc;
          margin: 30PX 0;
    
    
      }
      H3{
          margin-top: 10PX;
    
      }
      </style>
      