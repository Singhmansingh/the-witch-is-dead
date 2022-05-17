<template>
<div id="title-box" v-if="window.width <= 768">
            <h1>The Witch is Dead</h1>
            <hr>
            <h2>An RPG about MURDER</h2>
            <h3>by <a target="_blank" href="https://gshowitt.itch.io/">@gshowitt</a></h3>
        </div>
    <div id="header-container">
        <div id="title-box" v-if="window.width > 768">
            <h1>The Witch is Dead</h1>
            <hr>
            <h2>An RPG about MURDER</h2>
            <h3>by <a target="_blank" href="https://gshowitt.itch.io/">@gshowitt</a></h3>
        </div>
        <div id="scenario-box" v-if="window.width > 1200">
            <p>The Witch-Hunter has retreated to the Village, <strong>the COWARD</strong>. get him.</p>
            <a target="_blank" href="https://imgur.com/a/d8QZe">Here's how to play.</a>
        </div>
        <div id="setting-box">
            <div class="setting-component">
               <p>The Village is:</p>
               <select name="village" id="village">
                   <option value="" disabled selected>Select Village trait...</option>
                    <option v-for="(trait,index) in config.village" :key="trait" :value="villageTrait">{{index + 1}}. {{trait}}</option>
                </select>
            </div>
            <div class="setting-component">
               <p>The Witch-hunter is:</p>
               <select name="witch-hunter" id="witch-hunter">
                   <option value="" disabled selected>Select Witch-Hunter trait...</option>
                    <option v-for="(trait,index) in config.hunter" :key="trait" :value="hunterTrait">{{index + 1}}. {{trait}}</option>
                </select>
            </div>
        </div>
    </div>
</template>

<script>
import * as DATA from '../data.json';

export default {
    name:'HeaderComponent',
    setup(){
        const config = DATA;

        return {
            config,
        }
    },
    mounted(){
                    window.addEventListener('resize',()=> this.handleResize())

        this.handleResize()
    },
    data(){
        return{
            villageTrait: "",
            hunterTrait:"",
            window:{
                width: 0,
                height: 0
            }
        }
    },
    methods:{
        handleResize(){
            console.log("RESIZE")
            this.window.width = window.innerWidth;
            this.window.height = window.innerHeight;
        }
    }
}
</script>

<style lang="scss" scoped>
$backgroundColor: white;
$red: rgb(206, 0, 0);
@mixin border {
    border: 2px solid;
    box-sizing: border-box
}
#title-box {
    border: 8px solid $red;
    background: $backgroundColor;
    box-sizing: border-box;
    flex:2;
    display: flex;
    justify-content: space-evenly;
    flex-direction: column;
    h1,h2, h3 {
        margin: 0;
        align-items: center;
        justify-content: center;
        display: flex;
        flex:1;
    }
    h2 {
        font-size:1.5rem;
    }
    h3 {
        opacity: 0.5;
        font-size: 1rem;
    }
    hr {
        width: 70%;
        align-self: center;
        border-color:inherit;
        border-style: solid;
        border-width: 3px;
        margin: 0;
    }
    h1 {
        font-size: 2.5em;
    }

}

#scenario-box {
    flex:2;
    @include border();
    background:$backgroundColor;
    display: flex;
    justify-content: center;
    align-items: center ;
    flex-direction: column;
    p {
        padding: 20px;
        font-size: 1.4rem;
        line-height: 1.75rem;
        margin:0;
        strong {
            font-size: 1.75rem;
        }
    }
}

#setting-box {
    flex:4;
    background: $backgroundColor;
    @include border();
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    .setting-component {
        width: 50%;
        justify-content: center;
        gap: 10px;
        align-items: flex-start;
        display: flex;
        flex-direction: column;
        padding-left: 2%;
        p {
            margin:0;
            font-size: 1.5em;
            font-weight: bold;
        }

        select {
            width: 90%;
            height: 30%;
        }
    }
    
}

span {
    margin-left: 10pt;
    color: $red;
    font-weight: bold;
}
</style>