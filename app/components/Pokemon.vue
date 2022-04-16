<template>
    <GridLayout columns="*" rows="30, 50, *">
        <Label class="poke_title" row="0" text="Тут апишка с покемонами" />
        <SearchBar row="1" v-model="pokemonName" @submit="findPokemon()" />
        <Label row='2' v-if="errorCode == 404" :text="error"></Label>
        <FlexboxLayout row="2" v-if="pokemonInfo && !errorCode" flexDirection="column" justifyContent="center" alignItems="center">
            <Image :src='pokemonInfo.sprites.front_default' />
            <Label class="poke_name" :text="pokemonInfo.name"></Label>
        </FlexboxLayout>
    </GridLayout>
</template>

<script>
import { Http } from '@nativescript/core'

export default {
    data() {
        return{
            pokemonName: null,
            pokemonInfo: null,
            error: null,
            errorCode: null
        }
    },
    methods:{
        findPokemon(){
            let pokename = this.pokemonName.toLowerCase()
            Http.request({
                url: `https://pokeapi.co/api/v2/pokemon/${pokename}`,
                method: 'GET'
            })
            .then((result) => {
                if(result.statusCode == 200){
                    console.log(result.statusCode)
                    this.pokemonInfo = JSON.parse(JSON.stringify(result.content));
                }
                if(result.statusCode == 404){
                    this.errorCode = result.statusCode
                    this.error = 'Такого покемона нету'
                }
            })
            .catch((err)=>{
            })
        },
    }
}
</script>

<style>
    .poke_name{
        font-size: 18px;
    }
    .poke_title{
        font-size: 15px;
        text-align: center;
    }
</style>