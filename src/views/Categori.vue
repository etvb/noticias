<template>
    <div class="container mt-4">
  <p>{{$route.params.slug}}</p>

      <!-- <pre>{{vota}}</pre> -->
      <div class="row justify-content-center">
        <h1 class="w-100 h2">Real news, curated by real humans</h1>
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
        <h1 class="w-100 h2">Up-and-coming</h1>
        <h6>If these newsletters reach goal (or get a sponsorship), we´ll bring on expert writers and launch them. Vote for all your favorites:</h6>
      </div>

      <div class="row">
        <div class="col-sm-3 p-0 m-2" v-for="information in vota" :key="information.id">
          <ENews :pnew = "information"></ENews>
        </div>
      </div>


    </div>






</template>



<script>
import EModal from "@/components/EModal.vue";
import ENews from "@/components/ENews.vue";
import axios from 'axios';

export default {
//   name: "home",
  components: {
    EModal,
    ENews
    // HelloWorld
  },
  data(){
    return {
    //   acomodo:[],
      news: [],
    //   sub:[],
      suscrito:[],
      vota:[],
    //   vid:'kjhk',
      newsLatterSelecter:[],
      slug: this.$route.params.slug


      // tags: []
    }
  },
  created(){
    this.getNews()
    // this.getTags()
    // this.getVotes()
  },//los hooks se ejecutan solo la primera vez que se carga el componente, para revisar los cambios usamos watch
  watch:{
    '$route.params.slug': function(nvalor){
        this.slug=nvalor
        this.getNews()
    }

  },
  methods:{
    getNews(){
        // 'https://newsletters.academlo.com/api/v1/tags/tecnologia?include=newsletters'
        // process.env.VUE_APP_URL_TAGS+'/' + this.slug
      const news = process.env.VUE_APP_URL_TAGS+'/' + this.slug +'?include=newsletters'
        //eslint-disable-next-line no-console
        console.log(news)
      axios.get(news)
      .then(response =>{
        //eslint-disable-next-line no-console
        console.log(response.data);
        this.news=response.data.newsletters;
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
        alert('Error en nwes2')
      })
    },
    update(value){
      this.newsLatterSelecter= value
    }
    
  }
};
</script>