<template>
  <div class="projek">
    <div id = "myContainer">
      <div class="container-cover" v-if="hide"></div>
      <img src="@/assets/basket.png" id ="myAnimation">
      <img src="@/assets/ring.png" id="ringBasket" alt="">
    </div>
    <button class="btn-start" @click="trowBall">Click Me</button>
  </div>
</template>

<script>
export default {
  name: 'pojeksiBasket',
  data: () =>({
    hide:true,
  }),
  methods: {
    trowBall() {
      this.hide = false;
      const elem = document.getElementById('myAnimation');
      const v0 = 14;
      const angle = 60;
      const angleRad = (angle / 360) * (2 * Math.PI);
      const g = (-9.8);
      let t = 0;
      let dt = 0.01;
      const vx = v0 * Math.cos(angleRad);
      let vy = v0 * Math.sin(angleRad);
      const hRing = 190;
      const tHMax = vy / (-g);
      let x = 0;
      let y = 90;
      const lemparBola = setInterval(() => {
        vy += g * dt;
        y += vy * dt * 20;
        x += vx * dt * 20;
        t += dt;
        elem.style.bottom = `${y}px`;
        elem.style.left = `${x}px`;
        if (t >= tHMax && y < hRing) {
          clearInterval(lemparBola);
          vy = 0;
          t = 0;
          dt = 0.1;
          let tLast = -(Math.sqrt(2 * (hRing / -g)));
          let hAkhir = hRing;
          let vmax = Math.sqrt(2 * hAkhir * -g);
          const tau = 0.10;
          let fall = true;
          const bolaMantul = setInterval(() => {
            if (fall) {
              const hMantul = y + vy * dt - 0.5 * g * dt * dt;
              if (hMantul < 0) {
                t = tLast + 2 * Math.sqrt(2 * hAkhir / -g);
                fall = false;
                tLast = t + tau;
                y = 0;
              } else {
                t += dt;
                vy += g * dt;
                y = hMantul;
              }
            } else {
              t += tau;
              vmax *= 0.75;
              vy = vmax;
              fall = true;
              y = 0;
            }
            hAkhir = 0.5 * vmax / -g;
            elem.style.bottom = `${y}px`;
            if (hAkhir <= 0.1) { clearInterval(bolaMantul); }
          }, 20);
        }
      }, 20);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.projek{
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.btn-start{
  background: rgb(54, 219, 39);
  cursor: pointer;
  width: 150px;
  height: 50px;
  border: none;
  border-radius: 25px;
  font-size: 24px;
  z-index: 99;
}
.btn-start:active{
  background: rgb(43, 133, 35);
}
#myContainer {
  width: 400px;
  height: 80%;
  position: relative;
  border: inset 5px;
  margin-bottom: 25px;
  background: rgb(254, 255, 185);
}
.container-cover {
  position: absolute;
  width: 100%;
  height: 100%;
  margin-bottom: 25px;
  background: rgba(56, 56, 56, 0.911);
  z-index: 100;
}
#myAnimation {
  left: 0px;
  bottom: 90px;
  width: 50px;
  height: 50px;
  position: absolute;
  background-image: url("../assets/basket.png");
  z-index: 1;
}
#ringBasket{
  position: absolute;
  transform: scaleX(-1);
  filter: FlipH;
  -ms-filter: "FlipH";
  width: 80px;
  height: 80px;
  z-index: 2;
  left: 250px;
  bottom : 150px;
  position: absolute;
}
</style>
