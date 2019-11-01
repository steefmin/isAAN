<template>
  <div class="container">
    <Toggle v-on:toggle="setDial" />
    <VGauge
      :value="value"
      :minValue="minValue"
      :maxValue="maxValue"
      :gaugeValueClass="'hidden'"
      :options="options"
      :top="false"
      class="gauge"
    />
  </div>
</template>

<script>
    import Toggle from "./Toggle"
    import VGauge from "vgauge"
    export default {
        name: "GaugeCanvas",
        components: {VGauge, Toggle},
        data() {
            return {
                value: 5,
                setValue: 5,
                minValue: 0,
                maxValue: 100,
                ON_VALUE: 80,
                OFF_VALUE: 5,
                VARIANCE: 5,
                VARIANCE_INTERVAL: 500,
                options: {
                    angle: 0.10, // The span of the gauge arc
                    lineWidth: 0.5, // The line thickness
                    // radiusScale: 0.6, // Relative radius
                    pointer: {
                        length: 0.6, // // Relative to gauge radius
                        strokeWidth: 0.035, // The thickness
                        color: '#000000' // Fill color
                    },
                    limitMax: true,     // If false, max value increases automatically if value > maxValue
                    limitMin: true,     // If true, the min value of the gauge will be fixed
                    percentColors: [
                        [0.00, "#a9d70b"],
                        [0.50, "#a9d70b"],
                        [0.80, "#f9c802"],
                        [0.90, "#ff0000"]
                    ],
                    strokeColor: '#e5e6e9',  // to see which ones work best for you
                    generateGradient: true,
                    highDpiSupport: true,     // High resolution support
                    animationSpeed: 1,
                    renderTicks: {
                        divisions: 6,
                        divWidth: 1.1,
                        divLength: 0.7,
                        divColor: '#e5e6e9',
                        subDivisions: 0,
                        subLength: 0.5,
                        subWidth: 0.6,
                        subColor: '#666666'
                    },
                },
            }
        },
        methods: {
          setDial() {
              this.setValue = this.setValue === this.OFF_VALUE
                      ? this.ON_VALUE
                      : this.OFF_VALUE;
              this.varyDial();
          },
          varyDial() {
              this.value = this.setValue + this.randInt(this.VARIANCE);
          },
          randInt(variance) {
              return Math.floor(Math.random() * 2 * variance - variance);
          },
        },
        mounted() {
          setInterval(() => { this.varyDial() }, this.VARIANCE_INTERVAL);
        }
    }
</script>

<style scoped>
 .container{
    display: flex;
   flex-direction: column;
 }

 canvas {
   min-width: 224px;
   min-height: 190px;
   width: 30vw;
   height: 12vw;
 }

 .gauge >>> .hidden {
   display: none;
 }
</style>
