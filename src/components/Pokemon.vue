<template>
    <div id="pokemon">
        <div class="card">
            <div class="card-image">
                <figure>
                <img :src="curenteImg" alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                
                    <div class="media-content">
                        <p class="title is-4">{{ num }} - {{ name[0].toUpperCase()+name.slice(1)}}</p>
                        <p class="subtitle is-6">Tipo: {{ pokemon.type }}</p>
                    </div>
                </div>

                <div class="content">
                    <button @click="mudarSprite" class="button is-info">Mudar sprite</button>
                </div>
            </div>
        </div>

    </div>
</template>

<script>

import axios from 'axios'

export default {
    created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.curenteImg = this.pokemon.front;
            console.log(this.pokemon)
        })
    },

    data(){
        return{
            isfront: true,
            curenteImg: '',
            pokemon :{
                type: '',
                front: '',
                back: ''
            }
        }
    },

    props: {
        num: Number,
        name: String,
        url: String
    },
    methods: {
        mudarSprite: function(){
            if(this.isfront){
                this.isfront = false;
                this.curenteImg = this.pokemon.back;
            }
            else{
                this.isfront = true;
                this.curenteImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style>
    #pokemon{
        margin-top: 2%;
    }
</style>