<template>
  <div class="home">
    <div class="container mt-4">
      <!-- <pre>{{vota}}</pre> -->
      <div class="row justify-content-center">
        <h1 class="w-100 h3">Real news, curated by real humans</h1>
        <h6>Packed with the trends, news & links you need to be smart, informed, and ahead of the curve</h6>
      </div>
      
      <div class="row justify-content-between">
        <div class="col-sm-3 p-0 m-2 " v-for="information in suscrito" :key="information.id">
          <!-- <p>hola</p> -->
          <ENews :pnew = "information" @update="update"></ENews>
        </div>
          

        <EModal class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true" :newsLatter='newsLatterSelecter'></EModal>
      </div>

      <div class="row justify-content-center">
        <h1 class="w-100 h3">Up-and-coming</h1>
        <h6>If these newsletters reach goal (or get a sponsorship), we´ll bring on expert writers and launch them. Vote for all your favorites:</h6>
      </div>

      <div class="row justify-content-between">
        <div class="col-12 col-sm-3 p-0 m-2" v-for="information in vota" :key="information.id">
          <ENews :pnew = "information"></ENews>
        </div>
      </div>


    </div>

    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import EModal from "@/components/EModal.vue";
import ENews from "@/components/ENews.vue";
import axios from 'axios';

export default {
  name: "home",
  components: {
    EModal,
    ENews
    // HelloWorld
  },
  data(){
    return {
      news: [],
      sub:[],
      suscrito:[],
      vota:[],
      vid:'kjhk',
      newsLatterSelecter:[]


      // tags: []
    }
  },
  created(){
    this.getNews()
    // this.getTags()
    // this.getVotes()
  },
  methods:{
    getNews(){
      const news = process.env.VUE_APP_URL_NEWS
      axios.get(news)
      .then(response =>{
        //eslint-disable-next-line no-console
        console.log(response.data);
        this.news=response.data;
        //eslint-disable-next-line no-console
        // console.log(this.news)
        // filtro de la data los que ya estan subscritos
        this.suscrito = this.news.filter(arr=>{
          return arr.subscribed >= arr.target
        })
        // filtro los que son para votar
         this.vota = this.news.filter(arr=>{
           return arr.subscribed < arr.target
         })
      })
      .catch(()=>{
        alert('Error en nwes')
      })
    },
    update(value){

      // alert(value);

      this.newsLatterSelecter= value
    }
    /*REVISAR POR QUE NO FUNCIONO
    getVotes(){
      // console.log(this.news)
     let subscribers = this.news.filter(arr =>{
     //eslint-disable-next-line no-console
       console.log('dentro'+this.news)
        return (arr.subscribed == '0')
     });
     //eslint-disable-next-line no-console
    console.log(subscribers);
    this.sub = subscribers;

    }*/
  }
};
</script>
