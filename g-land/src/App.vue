<template>
  <div id="app">
    <HeaderComponent/>
    <HomePage />
  </div>
</template>

<script>

import HeaderComponent from './components/HeaderComponent.vue';
import HomePage from './components/HomePage.vue';
// import GreetingComponent from './components/GreetingComponent.vue';
 
export default {
  
  name: 'App',
  components: {
    HomePage,HeaderComponent
  },
};
</script>

<style>
/* Ваши стили */
</style>
