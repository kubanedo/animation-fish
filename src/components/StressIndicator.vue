<template>
<div class="stress-indicator">
  <div class="stress-indicator__text">Indikátor stresu v akváriu</div>  
  <div class="stress-indicator__bar" :class="{pulsate: stress === 4}">
      <div class="stress-indicator__inner" :style="{width: ((stress - 1) * 33.33) + '%' }">          
      </div>
  </div>   
</div>  
</template>

<script>
export default {
    props: {
        stress: {
            type: Number,
            default: 1
        }
    }
}
</script>

<style lang="scss" scoped>
.stress-indicator {
    margin: 1rem;
    width: 95%;
    max-width: 300px;

    &__text {
        margin-bottom: .3rem;
        font-weight: bold;
    }

    &__bar {
        border-radius: .5rem;
        background: white;
        overflow: hidden;
    }

    &__inner {
        height: 2rem;
        background: darkorange;
        transition: all 1s ease-in-out;
    }
}
.pulsate {
    animation: pulse 1s ease-in-out infinite;
    .stress-indicator__inner {
        background: red;
    }
}
@keyframes pulse {
    0% {
        transform: scale(1.0);
    }
    50% {
        transform: scale(1.1);
    }
    100% {
        transform: scale(1.0);
    }
}
</style>