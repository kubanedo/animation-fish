<template>
  <div ref="float">
      <slot />
  </div>
</template>

<script>
import { gsap, Sine, Back } from "gsap";

const rotate = (target) => {  
  gsap.to(target, {
    rotation: "random([4, 8])",
    ease: Back.easeInOut,
    duration: "random([5, 10])",
    repeat: -1,
    yoyo: true
  });
}

const moveX = (target) => {  
  gsap.to(target, {
    x: "random([10, 20])",
    ease: Sine.easeInOut,
    duration: "random([3, 5])",
    repeat: -1,
    yoyo: true
  });
}

const moveY = (target) => {  
  gsap.to(target, {
    y: "random([20, 30])",
    ease: Sine.easeInOut,
    duration: "random([3, 5])",
    repeat: -1,
    yoyo: true
  });
}

export default {
    mounted() {
        gsap.set(this.$refs.float, {
            x: "random([-20, -10])",
            y: "random([-30, -20])",
            rotation: "random([-8, -4])"
        });

        moveX(this.$refs.float);
        moveY(this.$refs.float);
        rotate(this.$refs.float);
    }
}
</script>

<style scoped>

</style>