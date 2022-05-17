<template>
<div id="player-sheet">
    <div id="top">
        <div id="sheet-left">
            <div id="about-container">
                <label for="name">Name:</label>
                <input type="text" id="name" placeholder="Enter Name Here..." :value="name" @change="e => name = e.target.value"/>
                <label for="species">Species:</label>
                <select name="species" id="species" @change="setStats($event)">
                    <option value="" disabled selected>Select your Species...</option>
                    <option v-for="(animal,index) in config.animals" :key="animal.species+id" :value="animal.species">{{index + 1}}. {{animal.species}}</option>
                </select>
            </div>
             <div id="stats-container">
               <div id="stats">
                   <div v-for="(value, stat) in stats" :key="stat+id" class="stat-bar">
                       <p>{{stat.toUpperCase()}}</p>
                       <div class="stat-box">{{value}}</div>
                   </div>
               </div>
               <div id="danger">
                   <p>CURRENT DANGER:</p>
                   <div id="danger-box" @click="manageDanger">{{danger}}</div>
               </div>
            </div>

        </div>
        <div id="sheet-right">
            <div id="portrait" @click="pressUploadDiv" :style="{backgroundImage: 'url('+img+')', opacity: img === 'fox.jpg' ? 0.8 : 1}"/>
            <input class="file-upload" type="file" accept="image/*" :id="'upload-'+id" @change="upload"/>

        </div> 
    </div>
    <div id="bottom">
        <div id="spell-container">
               <label for="species">Magic Spell You Know:</label>
               <select name="species" id="species">
                   <option value="" disabled selected>Select your spell...</option>
                    <option v-for="(spell, index) in config.spells" :key="spell+id" :value="spell">{{index + 1}}. {{spell}}</option>
                </select>
        </div>
    </div>
</div>
</template>

<script>
import * as DATA from '../data.json';
export default {
    name:'PlayerSheet',
    props:{
        id:String,
    },
    setup(){
        const config = DATA;
        return {
            config
        }
    },
    created(){
        let self = this;
        window.addEventListener('keydown', (e) => {
            if(e.key === "Shift") self.holdingShift = true
        })
         window.addEventListener('keyup', (e) => {
            if(e.key === "Shift") self.holdingShift = false
        })
    },
    data(){
        return {
            name:"",
            holdingShift: false,
            species:"",
            stats: {
                Clever: 0,
                Fierce: 0,
                Sly: 0,
                Quick: 0,
            },
            danger: 0,
            spell:"",
            img: "fox.jpg"
        }
    },

    methods:{
        setStats(e){
            let animal = this.config.animals.find(o => o.species === e.target.value);
            this.stats = {
                 Clever: animal.stats.c,
                Fierce: animal.stats.f,
                Sly: animal.stats.s,
                Quick: animal.stats.q,
            }
        },
        manageDanger(){
            if(this.holdingShift) {
                if(this.danger== 0) return;
                this.danger--;
            }
            else {
                 if(this.danger>= 6) return;
                this.danger++;
            }
        },
        pressUploadDiv(){
            console.log('click',this.id)
            document.getElementById('upload-'+this.id).click();
        },

        upload(e){
        let files = e.target.files || e.dataTransfer.files;
      if (!files.length) return;
      this.createImage(files[0]);
    },
    createImage(file) {
      let reader = new FileReader();
      let vm = this;
      reader.onload = (e) => {
        vm.img = e.target.result;
              console.log(vm.img);

      };
      reader.readAsDataURL(file);
    },

    }
}
</script>
<style lang="scss" scoped>

$flex-sizing: 32%;
$paddingSide: 3px 10px 3px 10px;
//$backgroundColor: rgb(255, 254, 242);
$backgroundColor: white;

@mixin side {
    flex:1;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    gap: 3px;
    div {
        justify-content: space-evenly;
        align-items: center;
        display: flex;
        flex-direction: column;
    }
}

@mixin border {
    border: 2px solid;
    box-sizing: border-box
}

#player-sheet {
    flex-basis: $flex-sizing;
    background: $backgroundColor;
height: 405px ;
    min-width: 455px;
    max-width: 650px;
    display:flex;
    flex-direction: column;

    
    #top {
        flex:4;
        box-sizing: border-box;
        display: flex;
        gap: 3px;

        #sheet-right {
            @include side();
            @include border();
            #portrait{
                flex:1;
                cursor: pointer;
                background-image: url("../assets/fox.jpg");
                background-position: center;
                background-size: contain;
                background-repeat: no-repeat;
            }
            .file-upload {
                display: none;
            }
        }

        #sheet-left {
            @include side();

            #about-container {
                @include border();
                flex:2;
                display: flex;
                justify-content: space-evenly;

                align-items: flex-start;
                padding:$paddingSide;

                input, select {
                    width: 100%;
                    padding: 0px;
                }

                
            }

            #stats-container {
                @include border();
                flex-direction: row !important;
                display: flex;
                flex:3;
                padding:  3px 3px 3px 10px;
                gap:3px;
                text-align: left;

                div {
                    height: 100%;

                }

                #stats {
                    flex:1;
                    display: flex;  
                        gap:4px;

                    .stat-bar {
                        flex-direction: row;
                        flex:1;
                        width: 100%;
                        height: 100%;
                        display:flex;
                        justify-content: space-between;
                        p {
                            margin:0px;
                            flex:2;
                        }
                        .stat-box {
                            @include border();
                            flex:1;
                            font-size: 1.5rem;
                            height: 100%;

                        }
                    }
                }

                #danger {
                    flex:1;
                    text-align: center;
                    justify-content: center;
                    display: flex;
                    align-items: center;
                    p {
                        padding: 3%;
                    }
                    #danger-box {
                        @include border();
                        width: 100%;
                        font-size: 2.5em;
                        user-select: none;
                        cursor: pointer;
                    }
                }
            }



        }
    }

    #bottom {
        
        display: flex;
        justify-content: stretch;
        padding-top: 3px;
        flex:1;

        #spell-container{
            @include border();
            flex:1;
            justify-content: space-evenly;
            padding:  $paddingSide;
            align-items: flex-start;
            display: flex;

            flex-direction: column;
            gap: 3px;
            p {
                margin:0;
                                                font-size: 0.75em;

            }
            select {
                width: 100%;
            }
    
        }
    }
}













</style>