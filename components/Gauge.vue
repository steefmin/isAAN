<template>
  <div class="container">
    <script src="https://bernii.github.io/gauge.js/dist/gauge.min.js" type="application/javascript" />
    <Spinner v-if="displaySpinner"/>
    <Toggle v-on:toggle="setDial" v-else/>
    <canvas id="gauge"></canvas>
  </div>
</template>

<script>
    import Spinner from "./Spinner";
    import Toggle from "./Toggle";
    export default {
        name: "GaugeCanvas",
        components: {Spinner, Toggle},
        data() {
            return {
                GaugeEl: null,
                value: 0,
                displaySpinner: true,
            };
        },
        methods: {
          getOpts() {
              return {
                  angle: 0.10, // The span of the gauge arc
                  lineWidth: 0.44, // The line thickness
                  radiusScale: 0.5, // Relative radius
                  pointer: {
                      length: 0.6, // // Relative to gauge radius
                      strokeWidth: 0.035, // The thickness
                      color: '#000000' // Fill color
                  },
                  limitMax: true,     // If false, max value increases automatically if value > maxValue
                  limitMin: true,     // If true, the min value of the gauge will be fixed
                  percentColors: [
                      [0.00, "#a9d70b" ],
                      [0.50, "#a9d70b" ],
                      [0.80, "#f9c802"],
                      [0.90, "#ff0000"]
                  ],
                  strokeColor: '#e5e6e9',  // to see which ones work best for you
                  generateGradient: true,
                  highDpiSupport: true,     // High resolution support
                  animationSpeed: 1,
                  // fontSize: 40,
                  renderTicks: {
                    divisions: 6,
                    divWidth: 1.1,
                    divLength: 0.7,
                    divColor: '#333333',
                    subDivisions: 0,
                    subLength: 0.5,
                    subWidth: 0.6,
                    subColor: '#666666'
                  },
              };
          },
          drawDial(options) {
              this.displaySpinner = false;
              let target = document.getElementById('gauge');
              this.GaugeEl = new Gauge(target).setOptions(options);
              this.GaugeEl.maxValue = 1000;
              this.GaugeEl.setMinValue(0);
              this.GaugeEl.set(this.value);
              setInterval(() => {this.varyDial()}, 500);

          },
          setDial() {
              this.value = this.value === 0 ? 800 : 0;
              this.GaugeEl.set(this.value);
          },
          varyDial() {
              this.GaugeEl.set(this.value + this.randInt(30));
          },
          randInt(val) {
              return Math.floor(Math.random() * 2 * val - val);
          },
          tryToMount() {
              if (typeof Gauge === "function") {
                  this.drawDial(this.getOpts());
              } else{
                  setTimeout(() => {this.tryToMount()}, 5000);
              }
          }
        },
        mounted() {
          this.tryToMount();
        }
    }
</script>

<style scoped>
 .container{
    display: flex;
   flex-direction: column;
 }

 canvas {
   width: 30vw;
   height: 12vw;
 }
</style>
