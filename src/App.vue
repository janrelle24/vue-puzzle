<template>
  <div v-if="status === 'beginning'" class="height-100 d-flex justify-content-center align-items-center" >
    <Start @start-game="startGame"/>
  </div>
  <div v-if="status === 'gaming'" class="height-100 d-flex justify-content-center align-items-center">
    <Game :size="size" @stop-game="stopGame"/>
  </div>
</template>

<script>

import Start from "./components/Start.vue";
import Game from "./components/Game.vue";

export default{
  name: "App",
  components: {
    Start,
    Game,
  },
  data(){
    return {
      status: "beginning",
      size: 3,
    };
  },
  methods: {
    startGame(size) {
      this.size = size;
      this.status = "gaming";
    },
  },
};
</script>

<style>
.height-100 {
  height: 100vh;
}
</style>

