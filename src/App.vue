<template>
  <div class="tank">
    <Bubble v-for="item in 15" :key="item"/>
    <StressIndicator :stress="stressLevel" /> 
    <Fish size="xs" fishColor="red" :stressLevel="stressLevel"/>         
    <Fish size="xs" fishColor="green" :stressLevel="stressLevel"/>
    <Fish size="md" fishColor="limegreen" :stressLevel="stressLevel"/>
    <Fish size="xs" fishColor="darkseagreen" :stressLevel="stressLevel"/>
    <Fish size="lg" ref="fish" :stressLevel="stressLevel"/>
    <button class="scare-fish"
      @click="scareTheFish"
      :disabled="stressLevel === 4"
      >{{buttonText}}</button>
  </div>  
</template>

<script>
import Fish from './components/Fish.vue'
import Bubble from './components/Bubble.vue'
import StressIndicator from './components/StressIndicator.vue'

export default {
  name: 'App',
  data() {
    return {
      stressLevel: 1
    }
  },
  components: {
    Fish,
    Bubble,
    StressIndicator
  },
  computed: {
    buttonText() {
      if(this.stressLevel < 2) {
        return "Vyplašit rybičky!"
      } else if(this.stressLevel < 3) {
        return "Ještě vyplašit rybičky!"
      } else if(this.stressLevel < 4) {
        return "Ještě VÍCE vyplašit rybičky!"
      } else {
        return "Už ne prosím. Taková krutost! 😢"
      }
    }
  },
  methods: {
    scareTheFish() {
      if(this.stressLevel < 4) {
        this.stressLevel++;
        setTimeout(this.calmTheFish, 10000);
      }
    },
    calmTheFish() {
      if(this.stressLevel > 1) {
        this.stressLevel--;
      }
    }
  }
}
</script>

<style lang="scss">
html {
  font-size: 12px;
  @media screen and (min-width: 640px) {
    font-size: 16px;
  }
}
body {
  margin: 0;
  font-family: 'Zilla Slab', serif;
}
.tank {
  position: relative;
  background: #8fe3ff;
  min-height: 100vh;
  overflow: hidden;
}
button.scare-fish {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  font-family: 'Zilla Slab', serif;
  cursor: pointer;
  font-weight: bold;
  font-size: 2rem;
  text-decoration: none;
  text-align: center;
  transition: all .5s ease; 
  display: block;
  padding: 1rem;
  border-radius: 1.5rem;
  background-color: lighten(#e3ae00, 4);
  color: white;
  transition: all .5s ease 0s; 
  box-shadow: 0 .625rem #e3ae00;  
  border: 0;

  &:hover, &:active {
    box-shadow: .187rem 1rem #e3ae00;
  }
  &:disabled {
    cursor: not-allowed;
    background-color: grey;
    box-shadow: 0 .625rem darken(grey, 5); 
  }
}
</style>
