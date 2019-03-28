<template>
  <div class="home">
    <Project/>
  </div>
</template>

<script>
// @ is an alias to /src
import Project from '@/components/ProjectBasket.vue';

export default {
  name: 'home',
  components: {
    Project,
  },
};
</script>

<style scoped>
  .home{
    width: 100%;
    height: 100%;
  }
</style>
