<template>
  <div class="home">
    <GeneratePdf msg="Welcome to Your Vue.js App"/>
   
  </div>
</template>

<script>
// @ is an alias to /src
import GeneratePdf from '@/components/GeneratePdf.vue'
 

export default {
  name: 'Home',
  components: {
    GeneratePdf,
  
  }
}
</script>
