<template>
  <div class="homepage">
    <div class="content">
      <div class="greeting-container" @click="toggleTileRow" v-if="!showTileRow">
        <GreetingComponent />
      </div>
      <div v-if="showTileRow" class="tile-row">
        <TileCardUxUi ref="tileCard0" class="tile-card" @mouseover="stopHoverEffect(0)" />
        <TileCardFrontend ref="tileCard1" class="tile-card" @mouseover="stopHoverEffect(1)" />
        <TileCardCovers ref="tileCard2" class="tile-card" @mouseover="stopHoverEffect(2)" />
      </div>
    </div>
  </div>
</template>

<script>
import GreetingComponent from './GreetingComponent.vue';
import g_bg from "../assets/g-bg.svg";
import TileCard from './TileCardUxUi.vue';
import TileCardFrontend from './TileCardFrontend.vue';
import TileCardUxUi from './TileCardUxUi.vue';
import TileCardCovers from './TileCardCovers.vue'

export default {
  name: 'HomePage',
  data() {
    return {
      showTileRow: false,
      image_bg: g_bg,
      intervalId: null,
      userHovered: false
    };
  },
  components: {
    GreetingComponent,
    TileCard,
    TileCardFrontend,
    TileCardUxUi,
    TileCardCovers
  },
  methods: {
    toggleTileRow() {
      this.showTileRow = !this.showTileRow;
      if (this.showTileRow) {
        this.startHoverEffect();
      } else {
        this.stopHoverEffect();
      }
    },
    startHoverEffect() {
      let index = 0;
      this.intervalId = setInterval(() => {
        if (!this.userHovered) {
          this.clearHoverEffects();
          const tileCard = this.$refs[`tileCard${index}`];
          if (tileCard) {
            tileCard.$el.classList.add('hover');
          }
          index = (index + 1) % 3; // Переход к следующей карточке (всего 3 карточки)
        }
      }, 2000); // Интервал в 2 секунды
    },
    stopHoverEffect(index) {
      this.userHovered = true;
      this.clearHoverEffects();
      const tileCard = this.$refs[`tileCard${index}`];
      if (tileCard) {
        tileCard.$el.classList.add('hover');
      }
      clearInterval(this.intervalId); // Остановить интервал
    },
    clearHoverEffects() {
      this.$refs.tileCard0.$el.classList.remove('hover');
      this.$refs.tileCard1.$el.classList.remove('hover');
      this.$refs.tileCard2.$el.classList.remove('hover');
    }
  },
  beforeUnmount() {
    clearInterval(this.intervalId);
  }
};
</script>

<style scoped>
.homepage {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  min-height: 100vh;
  background: 
    url('@/assets/g-bg.svg') no-repeat center center fixed,
    linear-gradient(rgba(0, 0, 0, 1), rgba(47, 73, 65, 1));
  background-size: cover;
  position: relative;
}
.greeting-container {
  padding: 500px;
}

.content {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  width: 100%;
  padding-top: 200px;
}

.greeting-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: auto;
  margin-top: 20px;
  cursor: pointer;
}

.tile-row {
  perspective: 1500px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  flex-wrap: wrap;
  transform-style: preserve-3d;
  transform: rotateY(-35deg) rotateZ(0deg) rotateX(45deg);
  margin-top: 20px;
}

.tile-card {
  margin: 10px;
  width: 200px;
  height: 300px;
  transform-style: preserve-3d;
  transition: transform 0.5s ease, box-shadow 0.5s ease;
}

.svg-image {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100%;
  z-index: -1;
}
</style>
