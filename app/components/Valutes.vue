<template>
    <GridLayout columns="*" rows="30, 100, 30, 30">
        <Label class="valute_title" row="0" text="Перевод иностранных валют в рубли" />
        <FlexboxLayout row="1" flexDirection="row" alignItems="center">
            <TextField  v-model="moneyNumber" @returnPress="valuteConvert()" hint="Введите количество валюты" keyboardType="number"></TextField>
            <ListPicker :items="allValutesNames" v-model="selectedValuteId" />
        </FlexboxLayout>
        <Label class="valute_label" v-if="convertedMoney" row="2" :text="`По курсу ${selectedValute} = ${selectedValuteCourse}`"></Label>
        <Label class="valute_label" v-if="convertedMoney" row="3" :text="`${moneyNumber} RUB = ${convertedMoney} ${selectedValute}`"></Label>
    </GridLayout>
</template>

<script>
    import { Http } from '@nativescript/core'

    export default {
        data() {
            return{
                valuteCourse: null,
                moneyNumber: null,
                convertedMoney: null,
                selectedValute: null,
                selectedValuteCourse: null,
                selectedValuteId: 0,
                allValutesNames: ['USD', 'EUR', 'AUD', 'AZN', 'GBP', 'BYN']
            }
        },
        methods:{
            getCurrVal(){
                Http.request({
                    url: "https://www.cbr-xml-daily.ru/daily_json.js",
                    method: 'GET'
                })
                .then((result) => {
                    this.valuteCourse = JSON.parse(JSON.stringify(result.content));
                })
            },
            valuteConvert(){
                if(this.moneyNumber){
                    this.selectedValute = this.allValutesNames[this.selectedValuteId];
                    this.selectedValuteCourse = this.valuteCourse.Valute[this.selectedValute].Value
                    this.convertedMoney = this.valuteCourse.Valute[this.selectedValute].Value * this.moneyNumber;
                }
            },
        },
        created(){
            this.getCurrVal();
        }
    }
</script>

<style>
    .valute_label{
        font-size: 15px;
    }
    .valute_title{
        font-size: 15px;
    }
</style>