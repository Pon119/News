<template lang="">
  <div>
    <NewsHeaderComponent/>
    <NewsGlobal/>
    <Topbutton/>
  
  </div>
</template>
<script>
import NewsGlobal from '@/components/NewsGlobal.vue';
import NewsHeaderComponent from '@/components/NewsHeaderComponent.vue';
import Topbutton from '@/components/Topbutton.vue';



export default {
  name: "AboutView",
  

  components: {
    NewsGlobal,  NewsHeaderComponent, Topbutton
  },
};
</script>
<style lang="">
  
</style>