<script>
import {store} from '../data/store'
  export default {
    data(){
      return{
        store
      }
    }
  }
</script>


<template>
  <div class="text-center my-5">
    <butto @click="store.counter++" class="btn btn-primary ">Incrementa contatore</butto>
  </div>
</template>



<style lang="scss" scoped>

</style>