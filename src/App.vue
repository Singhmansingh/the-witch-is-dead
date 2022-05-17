<template>
  <header-component/>
  <player-component/>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue';
import PlayerComponent from './components/PlayerComponent.vue';
export default {
  name: 'App',
  components: {
    'header-component': HeaderComponent,
    'player-component': PlayerComponent
  }
}
</script>

<style lang="scss">

$backgroundColor: rgb(255, 245, 221);
$textColor: #171717;

@mixin hideScrollbar {
  &::-webkit-scrollbar {
    width: 0 !important
  }
  -ms-overflow-style: none;
  scrollbar-width: none;
}

@font-face {
  font-family: "Cartoonist Hand";
  src: url('./assets/fonts/cartoonist-hand.ttf');
}

#app {
  font-family: "Cartoonist Hand";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  height: 100%;
  width: 100%;
  color: $textColor;
  border-color: $textColor;
  display: flex;
  flex-direction: column;
  scrollbar-width: none;
  box-sizing: border-box;
  font-size: 1.2em;
}

body {
  display: flex;
  margin:0;
  background: $backgroundColor;
    height: 100vh;
      width:100vw;

  overflow:hidden;
}

#player-container{
    @include hideScrollbar();

  display: flex;
  flex: 9;
  width: 100%;
  flex-direction: row;
  overflow-y: scroll;
  row-gap:12px;
  padding-bottom: 24px;
  padding-top: 24px;
  
  align-items: center;
  justify-content: space-evenly;
  flex-wrap: wrap;

}

#header-container{
  flex:2;
  display: flex;
  div{
          margin:15px;
          

  }
}

select, input {
  background: none;
  border-width: 0;
  border-bottom: 2px solid $textColor;
  font-family: inherit;
  color:inherit;
  font-size: inherit;
  cursor: pointer;
}

label {
  opacity: 0.5;
                      font-size: 0.75em;

}

option {
  background: darken($backgroundColor, 2%);
  font-family: "Cartoonist Hand";
}
</style>
