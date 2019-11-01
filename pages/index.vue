<template>
  <div class="main">
    <div class="header">
      <h2>Is {{ name }} AAN?</h2>
    </div>
    <div class="container">
      <Gauge/>
    </div>
    <div class="footer">
      <a href="https://steefmin.xyz">by: MINdustries</a>
    </div>
  </div>
</template>

<script>
import Gauge from '~/components/Gauge.vue'

export default {
  components: {
    Gauge
  },
    data() {
      return {
          name: this.getName()
      }
    },
    methods: {
      getName() {
          let re = /(\/|-|#)/g
          return this.$route.fullPath.replace('/', '').replace(re, ' ') || 'het feestje'
      }
    }
}
</script>

<style>
div {
  display: flex;
}

.main {
  flex-direction: column;
  align-items: center;
}

.container {
  justify-content: center;
}
.header {
  height: 10vh;
  padding: 50px;
}
.footer {
  align-items: flex-end;
  justify-content: right;
  height: 10vh;
}
a {
  font-size: 10pt;
  text-decoration: none;
  color: black;
}
</style>
