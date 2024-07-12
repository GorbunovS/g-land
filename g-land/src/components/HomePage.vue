<template>
  <div class="homepage">
    <HeaderComponent/>
    <div class="content">
      <div class="greeting-container">
        <GreetingComponent></GreetingComponent>
      </div>
      <img :src="image_bg" class="svg-image">
    </div>
  </div>
</template>

<script>
import GreetingComponent from './GreetingComponent.vue';
import HeaderComponent from './HeaderComponent.vue';
import g_bg from "../assets/g-bg.svg";

export default {
  name: 'HomePage',
  data() {
    return {
      image_bg: g_bg,
    };
  },
  components: {
    GreetingComponent,
    HeaderComponent
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

.content {
  position: relative; /* Добавлено для корректного позиционирования */
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  flex-grow: 1;
  width: 100%;
}

.greeting-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh; /* Выравнивание GreetingComponent по центру экрана */
}

.svg-image {
  width: 100%;
  height: 130vh;
  min-width: 700px;
  min-height: auto;
}
</style>
