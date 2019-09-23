<template>
  <div >
    <div :class="pnew.subscribed >= pnew.target ? '' : 'd-flex' ">
    <!-- <div class="rounded-circle"> -->
    <div class="mt-2 mr-1 d-flex justify-content-around">
      
      <div :class="pnew.subscribed>=pnew.target?'w-25' :'d-none'"></div>

      <div class="contenedorImg">
        <img :src="pnew.image" alt="foto" class="card-img-top flex-fill" />
      </div>

      <!-- <div class="w-25" :class="pnew.subscribed>=pnew.target ? ' ' : 'd-none' "></div> -->
      <div :class="pnew.subscribed>=pnew.target?'bgOrange text-white badge text-wrap text-center w-25 h-25' :'d-none' ">hola</div>
    </div>

    <!-- </div> -->
    <div class="card-body d-inline">
      <h5 class="card-title big mb-0 " v-text="pnew.title">titulo</h5>
      <p class="card-text midium" v-text="pnew.description">cuerpo</p>
    </div>
  </div>
   
  <!-- update es cualquier nombre de la funcion-->
    <button type="button" class="position-relative btn  w-100 btn-outline-dark" data-toggle="modal" 
    data-target="#exampleModal"
    @click="$emit('update',pnew)" 
    ><i :class="pnew.subscribed>=pnew.target?'fas fa-envelope':'fas fa-thumbs-up'"  class="position-absolute movido colorOrange"></i>{{pnew.subscribed>=pnew.target ? 'Subscribe' : 'vote'}} </button>
    <!-- seccion progreso -->
    <div :class="pnew.subscribed>=pnew.target?'d-none':''">
      <div class="progress my-3">
          <progress class="w-100" :value="pnew.subscribed" :max="pnew.target">70 %</progress>
          <!-- <div class="progress-bar" role="progressbar" style="width: 25%" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100"></div> -->
      </div>
      <div class="row justify-content-between mx-2">
        <div class="subscribe">
          <p class="mb-1" v-text="pnew.subscribed">2,955</p>
          <p class="small">SUBSCRIBED</p>
        </div>
        <div class="target">
          <p class="mb-1" v-text="pnew.target">3,000</p>
          <p class="small">TARGET</p>
        </div>
      </div>
    <!-- cierre seccion progreso -->
    </div>

  </div>
</template>

<script>
export default {
  props: ["pnew"]
 
  
}
</script>  

<style scoped>
    .contenedorImg{
        width: 75px;
        height: 75px;
        /* border: 1px solid red; */
        border-radius: 50%;
        overflow: hidden;

    }
    .contenedorImg img{
        width: 100%;
    }
    .small{
      font-size: .5rem;
    }
    .midium{
      font-size: .9rem;
    }
    .big{
      font-size: 1.1rem;
      font-weight: bold;
    }
    .bgOrange{
        background-color: #fd7e14;
    }
    .colorOrange{
        color: #fd7e14;
    }
    .movido{
      top: 11px;
      left: 16px;
    }

</style>