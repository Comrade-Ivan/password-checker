<template>
  <div class="my-2">
    <p class="my-1 status-text" :class="[textClass]"> {{ strength.message }}</p>
    <div class="progress" style="height: 5px;">
      <div class="progress-bar progress-bar-striped" :class="[bgClass]" :style="strength.style"></div>
    </div>
  </div>
</template>

<script>
  export default {
    props: ["state"],
    
    data() {
      return ({
      })
    },

    computed: {
      strength: function() {
        switch (this.state) {
          default: 
            return {message: "Пароль слишком короткий", colorPostfix: "-primary", style: {width: "5%"}, };
          case "strong":
            return {message: "Сильный пароль", colorPostfix: "-success", style: {width: "100%"}, };
          case "medium":
            return {message: "Средний пароль", colorPostfix: "-warning", style: {width: "65%"}, };
          case "weak":
            return {message: "Слабый пароль", colorPostfix: "-danger", style: {width: "25%"}, };
        }
      },
      bgClass: function() {
        return 'bg' + this.strength.colorPostfix;
      },
      textClass: function() {
        return 'text' + this.strength.colorPostfix;
      }
    }
  }
</script>

<style scoped>
  .progress-bar {
    transition: width .5s, background-color .2s;
    width: 35%;
  }
  .status-text {
    transition: color .2s;
  }
</style>