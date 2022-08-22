<template>

  <div id="pokemon">

    <div class="card">
        <div class="card-image">
            <figure>
                <img :src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-content">
                    <p class="title is-4">{{num}} - {{upper(name)}}</p>
                    <p class="subtitle is-6">{{pokemon.type}}</p>
                </div>
            </div>

            <div class="content">
                <button class="button is-medium is-fullwidth" @click="changeSprite">Mudar sprite</button>
            </div>
        </div>
    </div>
</div>

</template>

<script>

import axios from 'axios';

export default {

    data() {
        return {
            isFront: false,
            currentImg: '',
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },

    created: function() {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            this.currentImg = this.isfront ? this.pokemon.back : this.pokemon.front
            
            console.log(this.pokemon)
        })
    },

    props: {
        num: Number,
        name: String,
        url: String
    },

    methods: {

        //Primeira letra maiuscula do name
        upper: function(value) {

            //Priemiro pega a primeira letra e poem em maiusculo e depois faz concatenação com o resto do nome
            const newName = value[0].toUpperCase() + value.slice(1)
            return newName;
        },

        changeSprite: function() {
            this.isfront = !this.isfront
            this.currentImg = this.isfront ? this.pokemon.back : this.pokemon.front
        }
    }
}
</script>

<style>
    #pokemon {
        margin-top: 2%;
    }
</style>