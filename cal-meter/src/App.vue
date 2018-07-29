<template>
  <div id="app">
    <calMeter/>
  
  </div>
</template>

<script>
import calMeter from './components/calMeter.vue'

export default {
  name: 'app',
  components: {
    calMeter
  }
}
</script>

 <style lang="scss">
 body{
  background: linear-gradient(25deg, #FFEB3B, darken(#00BFA5, 10));
#app {

  margin: 3rem auto;
  height: 100vh;
  width: 100vw;
  width: 740px;
  background: linear-gradient(25deg, #FFEB3B, darken(#00BFA5, 10));
  border-radius: 10px;
}

}
</style>
