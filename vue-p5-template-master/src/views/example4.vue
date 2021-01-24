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
        var r=30;
        var t0;
        var t1;
        var t=0;var r0;
        var pi=3.1415926;

        p5.setup = () => {
            p5.createCanvas(w, h, p5.WEBGL);
        };

        p5.draw = () => {
            // p5.background(0);
            background(220); 
            for(var i=35;i>0;i--)
            {
              if(i%2==0)
              { 
                p5.fill(220);
                t0=p5.sin((t-(pi/35)*i)*4);
                if (t0>0)
                  r0=r*t0; 
                else 
                  r0=0;
                  p5.ellipse(200,200,r*i+r0);
              }
              else
              {
                p5.fill(50);
                p5.ellipse(200,200,r*i);
              } 
            }
        t+=0.01;
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