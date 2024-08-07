<script>
import {store} from '../data/store';
import todoListVue from './partials/todoList.vue';
  export default {
    data(){
      return{
        store
      }
    },
    components: {
      todoListVue,
    
  }
}
  
</script>


<template>
  <div class=" my-5">
    <todoListVue/>
  </div>
</template>



<style lang="scss" scoped>

</style>