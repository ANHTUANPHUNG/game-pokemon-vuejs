<template >
  <div class="container__main">
    <div class="screen">
      <h1>POKEMON MEMORIES</h1>
      <h3>Select</h3>
      <div class="modes">
        <div class="select__div" @click="onStart(16)">
          <div>4x4</div>
          <div>Easy</div>
        </div>
        <div  class="select__div" @click="onStart(36)">
          <div>6x6</div>
          <div>Normal</div>
        </div>
        <div  class="select__div" @click="onStart(64)">
          <div>8x8</div>
          <div>Hard</div>
        </div>
        <div  class="select__div" @click="onStart(100)">
          <div>10x10</div>
          <div>Super Hard</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
    export default {
        methods: {
            onStart(totalOfBlocks) {
                this.$emit("onStart", {totalOfBlocks})
            }
        }
    }
</script>
<style lang="css" scoped>
  .container__main{
    height: 100vh;
    display: flex;
    text-align: center;
    justify-content: center;
    align-items: center;
    color: white;
    background-color: #212121;
  }
  .modes {
    display: flex;
    width: 100%;
    height: 50px;
    justify-content: space-around;
    cursor: pointer;
  }
  .select__div{
    width: 90px;
    height: 90px;
    border: 1px solid white;
    border-radius: 20px;
    padding-top: 15px;
  }
</style>