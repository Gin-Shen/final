<template>
  <div class="container">
    <div class="p5Canvas"></div>
  </div>
</template>

<script>
import P5 from 'p5';

export default {
  data() {
    return {
      p5Canvas: null,
    }
  },
  created() {
    const sketch = p5 => {
        let w = 500;
        let h = 400;

        // let w = window.innerWidth;
        // let h = window.innerHeight;
        var img;
        let snowflakes = [];
        p5.preload = () =>{
            img=p5.loadImage("snowman.jpg");
        };
        p5.setup = () => {
            p5.createCanvas(w, h);
            p5.noStroke();
        };

        p5.draw = () => {
            p5.background(220);
            p5.imageMode(CENTER);
            p5.image(img,200,200);
            let t = p5.frameCount / 60; 
            for (let i = 0; i < p5.random(5); i++) {
              p5.snowflakes.push(new p5.snowflake()); 
            }
            for (let flake of p5.snowflakes) {
              flake.update(t); 
              flake.display(); 
            }

        };
        p5.snowflake = () =>{
          this.posX = 0;
          this.posY = p5.random(-50, 0);
          this.initialangle = p5.random(0, 2 * p5.PI);
          this.size = p5.random(2, 5);
          this.radius = p5.sqrt(p5.random(p5.pow(width / 2, 2)));

          this.update = function(time) {
          let w = 0.6; 
          let angle = w * time + this.initialangle;
          this.posX = width / 2 + this.radius * p5.sin(angle);
          this.posY += p5.pow(this.size, 0.5);
            if (this.posY > height) {
            let index = p5.snowflakes.indexOf(this);
            p5.snowflakes.splice(index, 1);
            }
          };

          this.display = function() {
            p5.ellipse(this.posX, this.posY, this.size);
          };
}
    }

    this.p5Canvas = new P5(sketch, 'p5Canvas');
  },
  unmounted () {
    this.p5Canvas = null;
  },
}
</script>

<style>
#p5Canvas {
  width: 100vw;
  position: relative;
}

main {
  margin: 0 auto;
  width: 90vw;
}
</style>