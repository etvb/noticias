<template>
<div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">


<div class="card modal-dialog" role="document">
    <!-- <div class="rounded-circle"> -->
    <div class="modal-content">
        <div class="modal-header">
        <!-- <h5 class="modal-title" id="exampleModalLabel">Modal title</h5> -->
        <div class="contenedorImg ml-auto">
          <img :src="newsLatter.image" alt="foto" class="card-img-top rounded-circle" />
        </div>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="card-body">
        <h5 class="card-title" >{{newsLatter.title}}</h5>
        <p class="card-text">{{newsLatter.description}}</p>
      </div>
      <form action="#">
        <div class="position-relative">
        <i class="position-absolute movido fas fa-envelope colorOrange "></i>
        <input class="w-100" type="text" placeholder="          Your email" />
        </div>
        <!-- <br> -->
        <a href class="btn btn-primary mt-2 w-100">SUBSCRIBE</a>
      </form>
    </div>
  </div>
</div>


</template>
<script>

export default {
  props:['newsLatter']
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
    .colorOrange{
        color: #fd7e14;
    }
    .movido{
      left: 15px;
      top: 7px;
    }
</style>