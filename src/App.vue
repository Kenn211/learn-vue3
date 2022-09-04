<script lang="ts">
import HeaderComp from './components/HeaderComp.vue'
import ContentComp from './components/ContentComp.vue';
export default {
    name: "App",
    components: {
        HeaderComp,
        ContentComp,
    },
};

</script>

<template>
  <div class="container m-5 p-2 rounded mx-auto bg-light shadow">
      <div class="main">
        <HeaderComp />
        <ContentComp></ContentComp>
      </div>
  </div>
</template>

<style scoped>
  

</style>
