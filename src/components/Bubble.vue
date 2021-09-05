<template>
  <div class="bubble" 
        ref="bubble" 
        :style="{width: size, height: size, bottom: '-' + size, opacity, left}"
        ></div>    
</template>

<script>
import { gsap } from "gsap";
import { MotionPathPlugin } from "gsap/MotionPathPlugin";
gsap.registerPlugin(MotionPathPlugin);

const randomNum = (min, max) => {
    return Math.random() * (max - min) + min;
}

let pathMaker = () => {
	let newPath = [
		{ x: 0, y: 0 },
		{ x: 50, y: -70 },
		{ x: -50, y: -140 },
		{ x: 0, y: -220 }
	];
	newPath.forEach((obj, i) => {
		obj.x = randomNum(-70, 70);
		obj.y = i * randomNum(-50, -100) + "vh";
	});
	return newPath;
};

const bubbleFloat = (bubble) => {
    const tl = gsap.timeline();
    tl.to(bubble, {
        duration: "random(2, 15)",
        delay: "random(.1, 1)",
        repeat: -1,
        scale: "random(1, 1.5)",
        motionPath: {
            path: pathMaker(),
            autoRotate: true
        }
    });
}


export default {
    data() {
        return {
            size: (this.randomNum(5, 8) / 10) + 'rem',
            opacity: this.randomNum(.3, .5),
            left: this.randomNum(1, 100) + '%'
        }
    },
    methods: {
        randomNum
    },
    mounted() {
        bubbleFloat(this.$refs.bubble);
    }
}
</script>

<style lang="scss" scoped>
.bubble {
    position: absolute;
    bottom: 0;
    background-color: white;
    height: 1rem;
    width: 1rem;
    border-radius: 50%;
}
</style>