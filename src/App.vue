<template>
  <!-- <div class="container">
    <users-list></users-list>
  </div>
  <div class="container">
    <div class="block" :class="{ animate: animatedBlock }"></div>
    <button @click="animateBlock">Animate</button>
  </div>
  <div class="container">
    <transition
      :css="no"
      name="para"
      mode="out-in"
      @before-enter="beforeEnter"
      @before-leave="beforeLeave"
      @enter="enter"
      @after-enter="afterEnter"
      @leave="leave"
      @enter-cancelled="enterCanceled"
      @leave-cancelled="leaveCanceled"
    >

      <p v-if="paraIsVisible">this is only sometimes visible</p>
    </transition>
    <button @click="showPara">Toggle Paragraph</button>
  </div>
  <div class="container">
    <transition name="fade-button">
      <button @click="showUsers" v-if="!usersAreVisible">show users</button>
      <button @click="hideUsers" v-else>hide users</button>
    </transition>
  </div>
  <base-modal @close="hideDialog" :open="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>
  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div> -->
  
  <router-view v-slot="slotProps">
      <transition name="route" mode="out-in">
<component :is="slotProps.Component"></component>
      </transition>
    </router-view>
</template>

<script>
// import UsersList from './components/ListData.vue';
export default {
  // components: { UsersList },
  data() {
    return {
      animatedBlock: false,
      dialogIsVisible: false,
      paraIsVisible: false,
      usersAreVisible: false,
      enterInterval: null,
      leaveInterval: null,
    };
  },
  methods: {
    enterCanceled(e) {
      clearInterval(this.enterInterval);
      console.log(e);
    },
    leaveCanceled(e) {
      clearInterval(this.leaveInterval);
      console.log(e);
    },
    animateBlock() {
      this.animatedBlock = !this.animatedBlock;
    },
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
    showPara() {
      this.paraIsVisible = !this.paraIsVisible;
    },
    showUsers() {
      this.usersAreVisible = true;
    },
    hideUsers() {
      this.usersAreVisible = false;
    },
    beforeEnter(e) {
      console.log('before enter');
      console.log(e);
      e.style.opacity = 0;
    },
    beforeLeave(e) {
      console.log('before leave');
      console.log(e);
      e.style.opacity = 0;
    },
    enter(e, done) {
      console.log('enter');
      console.log(e);
      let round = 1;
      this.enterInterval = setInterval(() => {
        e.style.opacity = round * 0.01;
        round++;
        if (round > 100) {
          clearInterval(this.enterInterval);
          done();
        }
      }, 20);
    },
    afterEnter(e) {
      console.log('afterEnter');
      console.log(e);
    },
    leave(e, done) {
      console.log('leave');
      console.log(e);
      let round = 100;
      this.leaveInterval = setInterval(() => {
        e.style.opacity = round * 0.01;
        round--;
        if (round === 0) {
          clearInterval(this.leaveInterval);
          done();
        }
      }, 20);
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}
.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
  /* transition:transform .3s ease-in-out */
}
.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}
.animate {
  /* transform:translateX(-150px) */
  animation: slide-fade 1s ease-out forwards;
}

/* .v-enter-from, .v-leave-to{
  opacity: 0;
  transform: translateY(-30px);
} */

.para-enter-active,
.para-leave-active {
  /* transition: all .3s ease-in-out; */
  animation: slide-fade 1s ease-out;
}

.fade-button-enter-from,
.fade-button-leave-to {
  opacity: 0;
}
.fade-button-enter-active {
  transition: opacity 1s ease-out;
}
.fade-button-enter-active {
  transition: opacity 1s ease-in;
}
.fade-button-enter-to,
.fade-button-leave-from {
  opacity: 1;
}

/* .v-enter-to, .v-leave-from{
  opacity: 1;
  transform: translateY(0);
} */

@keyframes slide-fade {
  0% {
    transform: translateX(0) scale(1);
  }
  70% {
    transform: translateX(100px) scale(1.1);
  }
  100% {
    transform: translateX(150px) scale(1.3);
  }
}
@keyframes opacity{
  from{
    opacity:0
  }
  to{
    opacity:1
  }
}
.route-enter-from{}
.route-enter-active{
  animation: opacity .3s ease;
}
.route-leave-active{
  animation: opacity .3s ease-in reverse;
}
.route-enter-to{}

</style>
