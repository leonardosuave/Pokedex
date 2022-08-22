<template>

  <div>
    <h1>{{num}} {{upper(name)}}</h1>
    <small>{{url}}</small>
  </div>

</template>

<script>
export default {
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