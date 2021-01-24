<template>
  <div class="container">
    <div id="p5Canvas"></div>
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

        p5.setup = () => {
            p5.createCanvas(w, h, WEBGL);
            p5.noStroke();
        };

        p5.draw = () => {
            p5.background(0);
            for (var i =1;i <3000; i++)
            {
              p5.drawcircle(255-0.1*i,255-0.1*i,255-0.1*i, i); 
              i++;
            }

        };
        p5.drawcircle = ( r, g, b, interval) =>{
        p5.fill(r, g, b);
        var x = 500; 
        var y = 500; 
        var t = p5.millis() /3+ interval *0.5;
        var xi;
        var yi;
        var radius = interval *15;
        xi = 0.01*radius * p5.Math.cos(t * Math.PI/180);
        yi = 0.01*radius * p5.Math.sin(t * Math.PI/180); 
        x += xi;
        y += yi;
        p5.ellipse(x, y, 20,20);
        };
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