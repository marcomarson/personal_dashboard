<template>
    <div class='row'>
         <!-- <q-card> -->
            <Mangatemplate v-for="manga in items" v-bind:key="manga" :manga="manga" >
            </Mangatemplate>
        <!-- </q-card> -->
       
    </div>
</template>

<script>
 import Mangatemplate from 'components/Mangatemplate'
export default {
    components: {
      Mangatemplate
    },
    name: 'PageIndex',
    data () {
        return {
            manga:true,
            items: [{
                title: 'Tales of Demons and Gods',
                stars: 4,
                last_episode: '164',
                image:"https://avt.mkklcdnv6.com/29/w/19-1583500265.jpg"
            },{
                title: 'Tales of Demons and Gods',
                stars: 4,
                last_episode: '164',
                image:"https://avt.mkklcdnv6.com/29/w/19-1583500265.jpg"
            },{
                title: 'Tales of Demons and Gods',
                stars: 4,
                last_episode: '164',
                image:"https://avt.mkklcdnv6.com/29/w/19-1583500265.jpg"
            },{
                title: 'Tales of Demons and Gods',
                stars: 4,
                last_episode: '164',
                image:"https://avt.mkklcdnv6.com/29/w/19-1583500265.jpg"
            },{
                title: 'Tales of Demons and Gods',
                stars: 4,
                last_episode: '164',
                image:"https://avt.mkklcdnv6.com/29/w/19-1583500265.jpg"
            },{
                title: 'Tales of Demons and Gods',
                stars: 4,
                last_episode: '164',
                image:"https://avt.mkklcdnv6.com/29/w/19-1583500265.jpg"
            }]
        }
    },
    methods:{
        loadData (){
            this.$axios.get('/api/backend').then((response) => {
                // this.data = response.data
                this.items = response.data
            })
            .catch(() => { //Error
                this.$q.notify({
                color: 'negative',
                position: 'top',
                message: 'Loading failed',
                icon: 'report_problem'
                })
            })
        }
    },
}
</script>
<style lang='scss'>

</style>
