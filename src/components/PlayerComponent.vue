<template>
    <div id="player-container">
            <PlayerSheet v-for="player in players" :key="'player-'+player" :id="'player-'+player" />

    </div>
</template>

<script>
import PlayerSheet from './PlayerSheet.vue';
export default {
    name:'PlayerComponent',
    components:{
        PlayerSheet,
    },
    mounted(){
        let self = this;
        window.addEventListener('keyup', (e) => {
            if(e.key == "[" && self.players > 1) self.players--;
            else if(e.key == "]") self.players++;
        })
    },
    data(){
        return {
            players: 1,

        }
    },
}
</script>