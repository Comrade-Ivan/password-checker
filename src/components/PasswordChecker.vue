<template>
  <transition name="fade">
    <div class="password-checker">
      <div class="form p-5 text-left">
        <hr class="my-3">
        <form>
          <div class="form-group">
            <label for="exampleInputEmail1">Введите пароль</label>
            <input type="email" class="form-control" v-model="password">
          </div>
          <PasswordIndicator v-bind:state="passwordStrength" />
          <div class="form-group">
            <label for="exampleInputPassword1">Повторите пароль</label>
            <input type="password" class="form-control" v-model="passwordCheck">
          </div>
          <p class="my-1" v-if="!message.hidden" :class="message.class">{{ message.text }}</p>
          <button type="submit" class="btn btn-primary">Submit</button>
        </form>
        <hr class="my-3">
      </div>
      <div class="background"></div>
    </div>
  </transition>
</template>

<script>
  import PasswordIndicator from './PasswordIndicator.vue'
  export default {
    components: {
      PasswordIndicator,
    },
    data() {
      return({
        password: "",
        passwordCheck: "",
        message: {class: "text-danger", text: "", hidden: true},
      });
    },

    computed: {
      passwordsSimilar: function() {
        return this.password == this.passwordCheck;
      },
      passwordStrength: function() {
        if (this.password.length < 5) {
          return "idle";
        }
        if (this.password.match(/((?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,15})/)) {
          return "strong";
        } else if (this.password.match(/((?=.*\d)(?=.*[a-z]).{8,15})/)) {
          return "medium";
        } else if (this.password.match(/((?=.*[a-z]).{6,15})/)) {
          return "weak";
        }
        return "idle";
      }
    }
  }
</script>

<style scoped>
.form {
  position: fixed;
  width: 45%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border: 1px solid lightsteelblue;
  border-radius: 15px;
  background: rgba(255,255,255,.9);
  z-index: 10000;
  box-shadow: 15px 15px 30px -5px rgba(150, 255, 255, 0.7);
}
.background {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  background-color: rgba(255, 255, 255, 0.7);
  z-index: 1000;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
</style>