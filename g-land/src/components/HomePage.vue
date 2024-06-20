<template>
    <div class="homepage">
      <div class="navbar">
        <GreetingComponent></GreetingComponent>
      </div>
      <div class="content">
        <!-- БЭКГРАУНД -->
        <img :src="image_bg" class="svg-image">
      </div>
    </div>
  </template>
  
  <script>
import GreetingComponent from './GreetingComponent.vue';
import g_bg from "../assets/g-bg.svg"
  export default {
    name: 'HomePage',
    data(){
      return{
        image_bg:g_bg,
      }
    },
    components: {
      GreetingComponent,
    },
  };
  </script>

  <style scoped>
  .homepage {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: linear-gradient(135deg, #000000 0%, #2F4941 100%);
  }
  
  .navbar {
    position: absolute;
    top: 20px;
    width: 100%;
    display: flex;
    justify-content: center;
  }
  
  .content {
    display: flex;
    justify-content: left;
    align-items: center;
    flex-grow: 1;
  }
  
  .svg-image {
    width: 100%;
    height: 130vh;
    min-width: 700px;
    min-height: auto;
    
  }
  </style>
  