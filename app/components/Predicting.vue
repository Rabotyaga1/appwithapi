<template>
    <GridLayout columns="*" rows="30, 100, 30">
        <Label class="predict_title" row="0" text="Узнайте возраст человека по имени" />
        <SearchBar row="1" v-model="personName" @submit="getNameInfo()" />
        <Label class="predict_label" v-if="nameInfo" row="2" :text="`Средний возраст людей с именем ${personName}: ` + nameInfo.age"></Label>
    </GridLayout>
</template>

<script>
import { Http } from '@nativescript/core'

export default {
    data() {
        return{
            personName: null,
            nameInfo: null,
        }
    },
    methods:{
        getNameInfo(){
            Http.request({
                url: `https://api.agify.io?name=${this.personName}`,
                method: 'GET'
            })
            .then((result) => {
                this.nameInfo = JSON.parse(JSON.stringify(result.content));
            })
        },
    }
}
</script>

<style>
    .predict_title{
        font-size: 15px;
    }
    .predict_label{
        font-size: 15px;
    }
</style>