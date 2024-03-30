<template>
 <!-- <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  -->
  <TopBanner/>
  <TicTacBoard/>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import TopBanner from './components/TopBanner.vue'
import TicTacBoard from './components/Tic-Tac-Board.vue'
export default {
  name: 'App',
  components: {
    TopBanner,
    TicTacBoard,
    //HelloWorld
  }
}
</script>

<style>

#app{
  min-height: 100vh;
display: flex;
flex-direction: column; 
}
.center_flex{
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
