<template>
    <div class="container__result">
        <div class="screen">
      <h1>Congratulations</h1>
      <p>{{ convertMillisecondsToSeconds(timer) }} seconds</p>
      <button @click ="onStartAgain" type="button" class="btn btn-primary">Start again</button>

    </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      timer: {
        type: Number,
        required: true
      }
    },
    methods: {
      convertMillisecondsToSeconds(milliseconds) {
        return Math.round(milliseconds / 1000);
      },
      onStartAgain() {
        this.$emit("onStartAgain")
      }
    }
  };
  </script>
  <style scoped>
    .container__result{
        height: 100vh;
    display: flex;
    text-align: center;
    justify-content: center;
    align-items: center;
    color: white;
    background-color: #212121;
    }
</style>
  