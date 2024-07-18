<template>
  <div class="homepage">
    <HeaderComponent />
    <div class="content">
      <div class="greeting-container" @click="toggleTileRow" v-if="!showTileRow">
        <GreetingComponent />
      </div>
      <div id="app" v-if="showTileRow" class="tile-row">
        <TileCard class="tile-card" />
        <TileCard class="tile-card" />
        <TileCard class="tile-card" />
      </div>
      <img :src="image_bg" class="svg-image" />
    </div>
  </div>
</template>

<script>
import GreetingComponent from './GreetingComponent.vue';
import HeaderComponent from './HeaderComponent.vue';
import g_bg from "../assets/g-bg.svg";
import TileCard from './TileCard.vue';

export default {
  name: 'HomePage',
  data() {
    return {
      showTileRow: false,
      image_bg: g_bg,
    };
  },
  components: {
    GreetingComponent,
    HeaderComponent,
    TileCard
  },
  methods: {
    toggleTileRow() {
      this.showTileRow = !this.showTileRow;
    }
  }
};
</script>

<style scoped>
.tile-row {
  perspective: 1500px; /* Пример значения перспективы */
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  transform-style: preserve-3d; /* Сохранение 3D-пространства для дочерних элементов */
  transform: rotateY(-45deg) rotateZ(15deg) rotateX(65deg); /* Поворот по оси Z и X */
  margin-top: 20px; /* Добавим небольшой верхний отступ для разделения с svg-image */
}


.tile-card {
  margin: 10px; /* Пример отступов между карточками */
  width: 200px; /* Пример размера карточки */
  height: 300px; /* Пример размера карточки */
  transform-style: preserve-3d; /* Сохранение 3D-пространства для дочерних элементов */
  transition: transform 0.5s ease; /* Плавное изменение поворота */
}

.homepage {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #000000 0%, #2F4941 100%);
}

.content {
  position: relative;
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
  height: 100vh;
  cursor: pointer; /* Добавляем указатель мыши для элемента, чтобы подчеркнуть его кликабельность */
}

.svg-image {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100%;
  z-index: -1; /* Чтобы изображение на заднем плане оставалось под остальными элементами */
}
</style>
