<template>
  <div id="app">
    <HomePage />
    <GreetingComponent/>
  </div>
</template>

<script>
import HomePage from './components/HomePage.vue';
import GreetingComponent from './components/GreetingComponent.vue';
 
export default {
  name: 'App',
  components: {
    HomePage,GreetingComponent
  },
};
</script>

<style>
/* Ваши стили */
</style>./components/Greeting.vue./components/GreetingComponent.vue
