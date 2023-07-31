<template>
  <div id="app">
    <BarangayForm />
  </div>
</template>

<script>
import BarangayForm from './components/BarangayForm.vue';

export default {
  name: 'App',
  components: {
    BarangayForm,
  },
};
</script>

<style lang="scss">
@import "~bulma/css/bulma.css";

@import url('https://fonts.googleapis.com/css2?family=Palanquin&family=REM&display=swap');


#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
  overflow-x: hidden;
  
}
</style>
