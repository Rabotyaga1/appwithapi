<template>
    <Page>
        <ActionBar>
            <Label text="Networking"/>
        </ActionBar>

        <GridLayout>
            <TabView selectedIndex="0">
                <TabViewItem title="Pokemons">
                    <Pokemon />
                </TabViewItem>
                <TabViewItem title="Valutes">
                    <Valutes />
                </TabViewItem>
                <TabViewItem title="Age">
                    <Predict />
                </TabViewItem>
            </TabView>
        </GridLayout>
    </Page>
</template>

<script>
    import Pokemon from './Pokemon.vue'
    import Valutes from './Valutes.vue'
    import Predict from './Predicting.vue'

    export default {
        computed: {
            
        },
        components:{
            Pokemon,
            Valutes,
            Predict 
        },
        data() {
            return{
                
            }
        },
        methods:{

        }
    }
</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';
</style>
