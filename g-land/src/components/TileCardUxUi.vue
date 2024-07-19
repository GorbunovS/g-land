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
        <!-- Добавляем три серых прямоугольника только для черной карточки -->
        <div v-if="card.color === 'tile-black' && hover" class="gray-rectangles">
          <div class="gray-rectangle-one"></div>
          <div class="gray-rectangle-two"></div>
          <div class="gray-rectangle-three"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hover: false,
      expandedIndex: -1,
      rotation: { x: 0, y: 0, z: 0 },
      hoverIntervalId: null,
      cards: [
        { color: 'tile-green', text: 'UX/UI' },
        { color: 'tile-white', text: 'UX/UI' },
        { color: 'tile-black', text: 'UX/UI' }
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
      const isExpanded = this.expandedIndex === index;
      const card = this.cards[index];

      const baseTransform = this.hover ? `translateZ(${index * 10}px)` : 'translateZ(0px)';
      const expandedTransform = isExpanded ? 'scale(2) translateZ(0)' : baseTransform;

      let boxShadow = '';
      if (card.color === 'tile-green' && this.hover) {
        boxShadow = '0 0 10px rgba(255, 255, 255, 0.5), 0 0 20px rgba(255, 255, 255, 0.3)';
      }

      return {
        transform: expandedTransform,
        opacity: this.hover || isExpanded || index === 0 ? 1 : 0,
        borderRadius: this.hover ? '15px' : '1',
        zIndex: isExpanded ? 2 : 1,
        boxShadow: boxShadow
      };
    },
    expandCard(index) {
      if (this.cards[index].color === 'tile-black') {
        this.expandedIndex = this.expandedIndex === index ? -1 : index;
        if (this.expandedIndex !== -1) {
          this.rotation.x = 0;
          this.rotation.y = 0;
          document.body.classList.add('fullscreen');
        } else {
          this.rotation.x = 50;
          this.rotation.y = 0;
          document.body.classList.remove('fullscreen');
        }
      } else {
        this.expandedIndex = this.expandedIndex === index ? -1 : index;
      }
    },
    startHoverEffect() {
      this.hoverIntervalId = setInterval(() => {
        this.hover = true;
        setTimeout(() => {
          this.hover = false;
        }, 500); // Устанавливаем hover в false через 0.5 секунды
      }, 7000); // Повторяем каждые 3 секунды
    }
  },
  mounted() {
    this.startHoverEffect();
  },
  beforeUnmount() {
    if (this.hoverIntervalId) {
      clearInterval(this.hoverIntervalId);
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
  height: 300px; /* Высота на ваш выбор */
}

.tile-stack {
  position: relative;
  width: 200px; /* Ширина на ваш выбор */
  height: 200px; /* Высота на ваш выбор */
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
  transition: transform 0.3s, opacity 0.3s, border-radius 0.8s, background-color 0.8s;
  cursor: pointer; /* Добавляем указатель при наведении, чтобы показать, что элемент кликабелен */
}

.tile-green {
  background-color: rgba(199, 231, 203, 0.128); /* Начально прозрачный фон */
  box-sizing: border-box; /* Устанавливаем box-sizing для корректного учета границы */
  border-radius: 15px;

  /* Градиентная линия */
  border-image: linear-gradient(to right, white, rgb(104, 104, 104), white) 1;
  border-image-slice: 30; /* Указываем толщину градиентной линии */
}

.tile-black {
  background-color: rgb(39, 39, 39);
  border: 2px solid transparent; /* Добавляем начально прозрачную обводку */
  transition: border-color 0.6s; /* Добавляем анимацию для обводки */
}

.tile-black:hover {
  border-color: rgba(255, 255, 255, 0.5); /* Показываем серую обводку при наведении */
}

.tile-white {
  background-color: rgb(255, 255, 255);
  box-shadow: 0 0 15px rgba(255, 255, 255, 0.5); /* Добавляем свечение (белая тень) */
}

.tile-text {
  color: white;
  font-size: 24px;
  font-family: 'TT runs', sans-serif;
  margin-left: 25px;
  position: absolute;
  z-index: 1; /* Гарантируем, что текст находится над другими элементами */
  transition: transform 0.8s;
  text-align: center;
}

.gray-rectangles {
  position: absolute;
  padding: 5px;
  bottom: 10px; /* Отступ от нижней грани карточки */
  left: 50%; /* Расположение в середине ширины карточки */
  transform: translateX(-50%); /* Центрируем по горизонтали */
  justify-content: space-between; /* Равномерное распределение прямоугольников */
  align-items: center;
  width: 80%;
  height: 80%;
}

.gray-rectangle-one, .gray-rectangle-two, .gray-rectangle-three {
  opacity: 0; /* Начально скрываем прямоугольники */
  transition: opacity 0.3s ease-in-out; /* Добавляем плавную анимацию появления */
}

.gray-rectangle-one {
  width: 0px; /* Ширина первого прямоугольника */
  height: 0px; /* Высота первого прямоугольника */
  border-radius: 10px;
  background-color: rgb(255, 255, 255); /* Серый цвет */
}
.gray-rectangle-two {
  width: 80px; /* Ширина второго прямоугольника */
  height: 20px; /* Высота второго прямоугольника */
  margin-top: 10px;
  border-radius: 5px;
  background-color: rgb(168, 168, 168); /* Серый цвет */
}
.gray-rectangle-three {
  width: 20px; 
  height: 8px; 
  border-radius: 2px;
  margin-top: 10px;
  background-color: rgb(2, 192, 68);
}

.tile:hover .gray-rectangle-one {
  opacity: 1; 
  width: 120px; /* Ширина первого прямоугольника */
  height: 100px;
  transition: all 0.3s ease-in-out;
}

.tile:hover .gray-rectangle-two {
  opacity: 1; 
  transition: all 0.9s;
}

.tile:hover .gray-rectangle-three {
  opacity: 1;
  transition: all 1.2s;
}

.fullscreen {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1000; /* Положение над остальными элементами */
  background-color: rgba(0, 0, 0, 0.8); /* Полупрозрачный черный фон */
  display: flex;
  justify-content: center;
  align-items: center;
}
.fullscreen .tile-container {
  height: 100vh; /* Занимаем всю высоту экрана */
  width: 100vw; /* Занимаем всю ширину экрана */
}

.fullscreen .tile-black {
  transform: none !important; /* Отменяем все трансформации */
  transform-origin: center center; /* Устанавливаем точку преобразования в центр */
  transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg); /* Устанавливаем rotation x и y в 0 */
}


.fullscreen .tile {
  width: 80%; /* Ширина увеличенной карточки */
  height: 80%; /* Высота увеличенной карточки */
  transform: none !important; /* Отменяем все трансформации */
  opacity: 1 !important; /* Убеждаемся, что элемент видим */
  border-radius: 0 !important; /* Убираем скругления */
  box-shadow: none !important; /* Убираем тень */
  transition: none; /* Отменяем все переходы */
}

.fullscreen .tile-text {
  font-size: 36px; /* Увеличиваем размер текста */
  margin-left: 0; /* Убираем отступы */
  color: white; /* Белый цвет текста */
}
</style>
