<template>
    <div class="logo">
      <img :src="logoSrc" alt="Logo" />
      <span>design</span>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      logoSrc: String,
    },
  };
  </script>
  
  <style scoped>
  .logo {
    display: flex;
    align-items: center;
  }
  
  .logo img {
    width: 40px;
    height: auto;
    margin-right: 10px;
  }
  
  .logo span {
    color: white;
  }
  </style>