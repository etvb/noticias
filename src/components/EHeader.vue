<template>
    <div class="container-fluid border px-5">
        <div class="row mt-3">
            <span class="flex-grow-1 text-left colorOrange h3">[INSIDE]</span>
            <!-- <div class="contenedorImg flex-grow-1 text-left">
                <img src="" alt="Logo">
            </div> -->
            <a class="mx-2" href="#">
                <i class="fas fa-search h3 colorOrange"></i>
            </a>
            <a class="mx-2" href="#">
                <i class="fas fa-user h3 colorOrange"></i>
            </a>

        </div>
        <div class="row">
                <router-link class="nav-link text-dark small text-muted" to="/">ALL</router-link>
                <!-- <a href="#" class="nav-link text-dark small">ALL-2</a> -->
            <div class="nav" v-for="tag in tags" :key="tag.slug">
                <router-link class="nav-link text-dark small text-muted" :to="'/categori/'+tag.slug">{{tag.name}}</router-link> 
            </div> 
        </div>
    </div>
    
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return{
            tags:[]
        }
    },
    created(){
        this.getTags()
    },
    methods: {

        getTags(){
            // const tags = process.env.VUE_APP_URL_TAGS
            axios('https://newsletters.academlo.com/api/v1/tags')
            .then(response =>{
                //eslint-disable-next-line no-console
                console.log(response.data)
                this.tags = response.data
            })
            .catch(()=>{
                alert('error en TAGS')
            })
    }
    }
    
}
</script>

<style scoped>
    .colorOrange{
        color: #fd7e14;
    }

</style>