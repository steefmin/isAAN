<template>
  <div class="main">
    <div class="header">
      <h2>Is{{name}} AAN?</h2>
    </div>
    <div class="container">
      <GaugeCanvas/>
    </div>
    <div class="footer">
      <a href="https://steefmin.xyz">steefmin</a>
    </div>
  </div>
</template>

<script>
import GaugeCanvas from '~/components/Gauge.vue'

export default {
  components: {
    GaugeCanvas
  },
    data() {
      let re = /[\/|-]/g;
      return {name: this.$route.fullPath.replace(re, ' ')}
    }
}
</script>

<style>
div {
  display: flex;
}

.main {
  flex-direction: column;
  /*justify-content: center;*/
  align-items: center;
}

.container {
  justify-content: center;
  /*min-height: vh;*/
  /*align-items: center;*/
  /*text-align: center;*/
}
.header {
  height: 10vh;
}
.footer {
  align-items: flex-end;
  height: 10vh;
}
a {
  font-size: 10pt;
}
</style>
