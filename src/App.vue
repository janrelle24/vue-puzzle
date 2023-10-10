<template>
  <div v-if="status === 'beginning'" class="height-100 d-flex justify-content-center align-items-center">
    <Start @start-game="startGame"/>
  </div>
</template>

<script>
import Start from "./components/Start.vue";

export default{
  name: "App",
  components: {
    Start
  },
  data(){
    return {
      status: "beginning",
      size: 3,
    }
  },
  methods: {

  }
}
</script>

<style>
.height-100 {
  height: 100vh;
}
</style>

