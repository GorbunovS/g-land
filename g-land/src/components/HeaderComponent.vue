<template>
  <div>
    <div :class="['header', { 'expanded': isExpanded }]">
      <LogoWhite :logoSrc="require('@/assets/g_logo_w.svg')" />
      <div class="nav-items" :class="{ 'expanded': isExpanded }">
        <span v-for="(item, index) in menuItems" :key="index"
              @mouseover="hoverItem = index"
              @mouseleave="hoverItem = null"
              @click="selectItem(index)"
              :class="{ 'active': selectedItem === index, 'hovered': hoverItem === index }"
              >{{ item }}</span>
      </div>
    </div>
    <button :style="{color: 'white'}" @click="toggleHeader">Отладка</button>
  </div>
</template>

<script>
import LogoWhite from './LogoWhite.vue';

export default {
  data() {
    return {
      isExpanded: false,
      menuItems: ['UX/UI', 'Frontend', 'Covers', 'Logofolio'],
      hoverItem: null,
      selectedItem: null
    };
  },
  components: {
    LogoWhite,
  },
  methods: {
    toggleHeader() {
      this.isExpanded = !this.isExpanded;
    },
    selectItem(index) {
      this.selectedItem = index;
      // Убрать следующую строку, чтобы меню не закрывалось при выборе пунктов
      // this.isExpanded = false;
    }
  },
};
</script>

<style scoped>
.header {
  font-family: "TT Runs Trial";
  font-size: 17px;
  font-style: normal;
  font-weight: 500;
  line-height: normal;
  display: flex;
  align-items: center;
  padding: 10px;
  transition: all 0.5s ease;
}

.nav-items {
  display: flex;
  overflow: hidden;
  white-space: nowrap;
  max-width: 0;
  opacity: 0;
  transition: max-width 0.5s ease, opacity 0.5s ease;
}

.nav-items.expanded {
  max-width: 500px; 
  opacity: 1;
}

.nav-items span {
  margin-left: 20px;
  color: white;
  cursor: pointer;
  padding: 5px 10px;
  transition: background-color 0.3s ease, color 0.3s ease, opacity 0.3s ease, transform 0.3s ease, font-weight 0.3s ease;
}

.nav-items span.active {
  font-weight: normal; /* Жирный шрифт для выбранного пункта */
  background-color: white;
  color: black;
}

.nav-items span.hovered {
  background-color: #1fd725; /* Зеленый фон на ховере */
  transform: scale(1.05); /* Увеличение размера при ховере */
  z-index: 1; /* Поднять над остальными пунктами */
}
</style>
