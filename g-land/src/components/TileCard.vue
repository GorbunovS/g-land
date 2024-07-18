<template>
  <div class="tile-container" 
       @mouseover="hover = true" 
       @mouseleave="hover = false"
       @click="expandCard">
    <div :class="['tile-stack', { 'tile-hover': hover }]" 
         :style="stackStyle">
      <div v-for="(card, index) in cards" 
           :key="index" 
           :class="['tile', card.color]" 
           :style="cardStyle(index)">
        <span v-if="card.text" class="tile-text">{{ card.text }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hover: false,
      expanded: false,
      rotation: { x: 50, y: 0, z: 50 },
      cards: [
        { color: 'tile-green', text: 'UX/UI' },
        { color: 'tile-white' },
        { color: 'tile-black' }
      ]
    };
  },
  computed: {
    stackStyle() {
      return {
        transform: `rotateX(${this.rotation.x}deg) rotateY(${this.rotation.y}deg) rotateZ(${this.rotation.z}deg)`
      };
    }
  },
  methods: {
    cardStyle(index) {
      if (!this.hover && index > 0) {
        return {
          opacity: 0,
          transform: 'translateZ(0px)'
        };
      }

      const baseTransform = this.hover ? `translateZ(${index * 10}px)` : 'translateZ(0px)';
      const expandedTransform = this.expanded ? 'scale(2) translateZ(0)' : baseTransform;

      return {
        transform: expandedTransform,
        opacity: this.hover || index === 0 ? 1 : 0,
        borderRadius: this.hover ? '15px' : '0',
        backgroundColor: this.hover || index === 0 ? '' : '#2F4941'
      };
    },
    expandCard() {
      this.expanded = !this.expanded;
    }
  }
};
</script>

<style scoped>
.tile-container {
  perspective: 1000px;
  margin: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 300px; /* Adjust as needed */
}

.tile-stack {
  position: relative;
  width: 200px; /* Adjust as needed */
  height: 200px; /* Adjust as needed */
  transform-style: preserve-3d;
  transition: transform 0.8s;
}

.tile-hover {
  transform: translateY(-20px);
}

.tile {
  width: 100%;
  height: 100%;
  position: absolute;
  backface-visibility: hidden;
  transition: transform 0.8s, opacity 0.8s, border-radius 0.8s, background-color 0.8s;
}

.tile-red {
  background-color: red;
}

.tile-green {
  background-color: green;
}

.tile-blue {
  background-color: blue;
}

.tile-white {
  background-color: white;
  box-shadow: 0 0 15px rgba(255, 255, 255, 0.5);
}

.tile-black {
  background-color: black;
}

.tile-text {
  color: white;
  font-size: 24px;
  text-align: center;
  line-height: 200px; /* Same as tile height */
}
</style>
