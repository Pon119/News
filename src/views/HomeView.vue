<template>
  <div class="home">
    <NewsHeaderComponent/>
    <NewsArticle/>
    <Topbutton/>
  </div>
</template>

<script>
import NewsArticle from '@/components/NewsArticle.vue';
import NewsHeaderComponent from '@/components/NewsHeaderComponent.vue';
import Topbutton from '@/components/Topbutton.vue';


// @ is an alias to /src


export default {
  name: "HomeView",
  components: {
    NewsArticle, NewsHeaderComponent, Topbutton
  },
};
</script>
