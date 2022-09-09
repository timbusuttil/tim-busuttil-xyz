<template>
  <div id="background-gradient" :style="backgroundStyle" @pointermove="pointerMove" ref="gradient">
    <div v-if="showDebug">
      <pre>x:<br>{{ params.x.true }}<br>{{ params.x.target }}<br>{{ params.x.current }}</pre>
      <pre>y:<br>{{ params.y.true }}<br>{{ params.y.target }}<br>{{ params.y.current }}</pre>
      <pre>m:<br>{{ params.m.true }}<br>{{ params.m.target }}<br>{{ params.m.current }}</pre>
      <pre>s:<br>{{ params.s.true }}<br>{{ params.s.target }}<br>{{ params.s.current }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BackgroundGradient',
  data() {
    return {
      showDebug: true,
      params: {
        x: { true: 0, target: 0, current: 0 },
        y: { true: 0, target: 0, current: 0 },
        m: { true: 0, target: 0, current: 0 },
        s: { true: 0, target: 0, current: 0 },
      },
      colours: [
        { name: 'gold', hex: '#ffd700' },
        { name: 'dodgerblue', hex: '#1e90ff' },
        { name: 'pink', hex: '#ffc0cb' },
        { name: 'mediumseagreen', hex: '#3cb371' },
      ]
    }
  },
  computed: {
    backgroundStyle() {

      return {
        background: `
          linear-gradient(${this.params.x.target * 360}deg, ${this.colours[0].hex}, ${this.colours[0].hex}00 70%),
          linear-gradient(${this.params.y.target * 360}deg, ${this.colours[1].hex}, ${this.colours[1].hex}00 70%),
          linear-gradient(${this.params.m.target * 360}deg, ${this.colours[2].hex}, ${this.colours[2].hex}00 70%),
          linear-gradient(${this.params.s.target * 360}deg, ${this.colours[3].hex}, ${this.colours[3].hex}00 70%)
        `
      }
    }
  },
  methods: {
    pointerMove(e) {
      this.params.x = {
        true: e.clientX,
        target: e.clientX / this.$refs.gradient.clientWidth
      }
      this.params.y = {
        true: e.clientY,
        target: e.clientY / this.$refs.gradient.clientHeight
      }
    },
    getTime() {
      let date = new Date();
      let mins = date.getMinutes();
      let secs = date.getSeconds();
      this.params.m = {
        true: mins,
        target: mins / 60
      }
      this.params.s = {
        true: secs,
        target: secs / 60
      }
    },
    animate() {
      // window.requestAnimationFrame(this.animate());
    }
  },
  created() {
    setInterval(() => this.getTime(), 1000);
    // window.requestAnimationFrame(this.animate());
  }
}
</script>

<style lang="scss">
#background-gradient {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  min-height: 100vh;
  /* mobile viewport bug fix */
  min-height: -webkit-fill-available;

  z-index: -1;
}
</style>
