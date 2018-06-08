<template>
  <div  class="">
    <button @click="changeLanguageENG()">ENG</button>
    <button @click="changeLanguageSRB()">SRB</button>
    <ul>
      <li v-for="video in info" 
      v-bind:key="video.youtubeId">      
      <img :src="generateThumbnailUrl(video.youtubeId)" alt="">
      <a href="">{{video.title}}</a>

     </li>
    </ul>

    </div>
</template>

<script>

export default {
  name: 'duoLingual',
  data(){
    return{ 
        info:[],
        url:'https://api.myjson.com/bins/13mms5',
        urlSRB: "https://api.myjson.com/bins/99ixh",
        urlENG: "https://api.myjson.com/bins/13mms5"
    }
  },
mounted(){

if(agCookie.read("language") === "english"){
  this.axios.get(this.urlENG).then(response => {
  this.info = response.data.videos;
      
    })}else{
  this.axios.get(this.urlSRB).then(response => {
  this.info = response.data.videos;
      
    })}
},
methods:{

    generateThumbnailUrl(id){
      return youtube.generateThumbnailUrl(id)
    },
    createCookie(name, value, days){
      agCookie.create(name,value,days);
    },
     readCookie(name){
      return agCookie.read(name);
    },
    changeLanguageSRB(){
      this.url = this.urlSRB;
      this.axios.get(this.url).then(response => {
      this.info = response.data.videos;
        })
       agCookie.create("language","serbian",10);


    },
    changeLanguageENG(){
    this.url = this.urlENG;
     this.axios.get(this.url).then(response => {
      this.info = response.data.videos;
        })
      agCookie.create("language","english",10);


    }

}

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
div{
//   max-width:800px;
//  margin:0 auto;
  button{
    // float:right;
    margin: 15px 0;
    background: lightseagreen;
    border: none;
    color: #fff;
    margin-left: 5px;
    padding: 10px 20px;
    border-radius: 10px;
    font-weight: bold;
    transition: 0.4s ease;
    &:hover{
      padding:11px 21px;
      background-color: #EFF6EE;
      color:lightseagreen;
    }
  }
  ul{
    list-style-type: none;
     text-align: left;
     padding: 0;

     li{
       display: flex;
       align-items: center;
       margin-bottom: 20px;
       background: #EFF6EE;
       width: 100%;
       transition: 0.5s all;
       border-radius: 20px;
      &:hover{
        background-color: lightseagreen;
        width:90%;
      } &:hover>a{
        color:#EFF6EE
      }
      &:hover{
        img{
          width:150px;
          transition:1s ease;
        }
      }
       a{
         margin-left: 50px;
         color: lightseagreen;
         text-decoration: none;
         font-weight: bold;
         font-size: 20px;
       
       }

       
       img{
         width: 100px;
         border: 2px solid lightseagreen;
        border-radius: 20px;
       }
     }

  }
}

</style>
