<template>
    <div class='row'>
        <div class ='col-6 q-pa-md manga'>
            <q-card>
                <div class ='row'>
                    <div class ='col-6'>
                        <img
                        alt="Quasar logo"
                        src="https://cdn.quasar.dev/logo/svg/quasar-logo.svg"
                        >
                    </div>
                    <div class ='col-6'>
                        <div class ='title'>
                            {{this.manga.title}}
                        </div>
                        <div class ='sub-title'>
                            {{this.manga.stars}}
                        </div>
                        <div class ='sub-title'>
                            {{this.manga.last_episode}}
                        </div>
                    </div>
                </div>
            </q-card>
        </div>
        <div class ='col-6 q-pa-md'>
            <q-card>
                <img
                alt="Quasar logo"
                src="https://cdn.quasar.dev/logo/svg/quasar-logo.svg"
                >
            </q-card>
        </div>
    </div>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
        return {
            manga: {
                title: '',
                stars: 4,
                last_episode: ''
            }
        }
    },
}
</script>
<style lang='scss'>

</style>
