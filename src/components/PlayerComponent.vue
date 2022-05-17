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
    data(){
        return {
            players: 6,

        }
    }
}
</script>