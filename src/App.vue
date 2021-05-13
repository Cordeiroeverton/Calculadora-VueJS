
<template>
  <div id="app">
    <h1>Calculadora</h1>
    <Calculator />
  </div>
</template>

<script>

import Calculator from "./main/Calculator"

export default {

  // eslint-disable-next-line vue/no-unused-components
  components: { Calculator }
}
</script>

<style>

  @font-face {
    font-family:"RobotoMono";
    src: url("./fonts/RobotoMono-VariableFont_wght.ttf");
  }

  * {
    font-family: "RobotoMono", monospace;
  }

  body {
    margin: 0;
  }
 
  #app {
    display: flex;
    flex-direction: column;
    height: 100vh;
    justify-content: center;
    align-items: center;
    text-align: center;

    color: rgb(0, 0, 0);
    background: linear-gradient(to right, rgb(83, 105, 118), rgb(41, 46, 73));
    
  }
  
</style>
