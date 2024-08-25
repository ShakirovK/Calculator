<script setup>
import { ref } from 'vue';
const display = ref('');
const buttons = [
  {value: 'AC', type: 'clear'},
  {value: 'DEL', type: 'delete'},
  {value: '.', type: 'operator'},
  {value: '/', type: 'operator'},
  {value: '7'},
  {value: '8'},
  {value: '9'},
  {value: '*', type: 'operator'},
  {value: '4'},
  {value: '5'},
  {value: '6'},
  {value: '-', type: 'operator'},
  {value: '1'},
  {value: '2'},
  {value: '3'},
  {value: '+', type: 'operator'},
  {value: '000'},
  {value: '00'},
  {value: '0'},
  {value: '=', type: 'equals'},
]
const update = (value) => {
  

  if (value == 'AC') {
    display.value='';
  }
  else if (value == 'DEL') {
    display.value = String(display.value).slice(0,-1);
  }
  else if (value == '=') {
    if (isNaN(String(display.value).slice(-1))) {
      display.value = String(display.value).slice(0,-1);
    }
    display.value = eval(display.value);
  }
  else if (isNaN(value) && isNaN(String(display.value).slice(-1))) {
    display.value = String(display.value).slice(0,-1);
    display.value += value;
  }
  else {
    display.value += value;
  }
};
</script>

<template>
  <div class="calculator">
    <input type="text" v-model="display" class="display" disabled>
    <div class="buttons">
      <button
        v-for="btn in buttons"
        :key="btn.value"
        @click="update(btn.value)"
        :class="`button button_${btn.type || 'default'}`"
      >
        {{ btn.value }}
      </button>
    </div>
  </div>
</template>

<style scoped>

/* Контейнер калькулятора */
.calculator {
  width: 300px;
  margin: 50px auto;
  padding: 20px;
  background-color: #d3d3d3;
  border-radius: 15px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
}

/* Стиль дисплея */
.display {
  width: 100%;
  height: 50px;
  margin-bottom: 15px;
  padding: 10px;
  font-size: 1.5rem;
  text-align: right;
  border: none;
  border-radius: 8px;
  background-color: #ffffff;
  box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.1);
  color: #333;
}

/* Сетка кнопок */
.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

/* Общий стиль кнопок */
.button {
  padding: 15px;
  font-size: 1.2rem;
  font-weight: bold;
  border: none;
  border-radius: 8px;
  background-color: #e0e0e0;
  color: #333;
  cursor: pointer;
  transition: background-color 0.2s, transform 0.1s;
}

/* Стили для различных типов кнопок */
.button_clear {
  background-color: #ff7675;
  color: #fff;
}

.button_delete {
  background-color: #fdcb6e;
  color: #fff;
}

.button_operator {
  background-color: #74b9ff;
  color: #fff;
}

.button_equals {
  background-color: #55efc4;
  color: #fff;
}

/* Эффекты при наведении и нажатии */
.button:hover {
  background-color: #d1d1d1;
}

.button_clear:hover {
  background-color: #ff6b6b;
}

.button_delete:hover {
  background-color: #e1b12c;
}

.button_operator:hover {
  background-color: #4aa3ff;
}

.button_equals:hover {
  background-color: #2bcbba;
}

.button:active {
  transform: scale(0.98);
}
</style>
