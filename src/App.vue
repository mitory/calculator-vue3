<template>
  <div class="calculator">
    <input type="text" v-model="display" class="display" disabled />
    <div class="buttons">
      <button v-for="button in buttons" 
          :key="button.value" 
          class="button" 
          @click="update(button)">
          {{ button.value }}
      </button>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const display = ref('');
    const buttons = [
      { value: 'AC', type: 'clear'},
      { value: 'DEL', type: 'delete'},
      { value: '%', type: 'operator'},
      { value: '/', type: 'operator'},

      { value: '7'},
      { value: '8'},
      { value: '9'},
      { value: '*', type: 'operator'},

      { value: '4'},
      { value: '5'},
      { value: '6'},
      { value: '-', type: 'operator'},

      { value: '1'},
      { value: '2'},
      { value: '3'},
      { value: '+', type: 'operator'},

      { value: '000'},
      { value: '0'},
      { value: '.', type: 'operator'},
      { value: '=', type: 'equals'},
    ]
    const update = (button) => {
      if(button.type === 'operator') {
        if(['.', '/', '*', '-', '+'].includes(display.value.slice(-1)) || !display.value.length) return;
      }

      switch(button.value) {
        case 'AC': 
          return display.value = '';
        case 'DEL':
          return display.value = display.value.slice(0, -1);
        case '=':
          if(!display.value.length) return '';
          return display.value = String(eval(display.value));
        default:
          return display.value += button.value;
          
} 
    }
    return {
      display, buttons, update
    }
  } 
}

</script>

<style scoped>
  * {
    margin: 0;
    padding: 0;
  }
  body, html {
    background: #123;
  }
  .calculator {
    width: 300px;
    height: 470px;
    margin: 0 auto;
    background: #654;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 1em 0;
    box-sizing: border-box;
  }
  .buttons {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 2px;
  }
  .button {
    width: 70px;
    height: 70px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
  }
  .button:hover,
  .button:focus {
    border: 1px solid white;
  }
  .display {
    height: 30px;
    padding: 10px;
    width: 70%;
    margin: 0 auto;
    font-size: 20px;
    border-radius: 10px;
    text-align: center;
  }
</style>
