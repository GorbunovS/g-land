<template>
    <div class="homepage">
      <div class="navbar">
        <!-- Навигация -->
      </div>
      <div class="content">
        <!-- БЭКГРАУНД -->
        <img src="@/assets/g-bg.svg" alt="SVG Image" class="svg-image">
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'HomePage',
  };
  </script>
  
  <style scoped>
  .homepage {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: linear-gradient(135deg, #000000 0%, #7B7068 100%);
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
    justify-content: center;
    align-items: center;
    flex-grow: 1;
  }
  
  .svg-image {
    width: 100%;
    height: 100%;
  }
  </style>
  