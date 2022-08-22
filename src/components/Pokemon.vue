<template>

  <div>
    <h1>{{num}} {{upper(name)}}</h1>
    <small>{{url}}</small>
  </div>

</template>

<script>

import axios from 'axios';

export default {

    data() {
        return {
            pokemon: {}
        }
    },

    created: function() {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            
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
            
        }
    }
}
</script>

<style>

</style>